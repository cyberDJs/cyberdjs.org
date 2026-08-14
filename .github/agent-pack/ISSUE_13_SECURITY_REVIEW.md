# Issue #13 Security Review - CyberDJs.org

Scope: focused security review for the current static `cyberdjs.org` site.

This review was limited to Issue #13 and the files explicitly allowed by the task:

- `AGENTS.md`
- `README.md`
- `.github/workflows/deploy.yml`
- `.github/agent-pack/ISSUE_01_AUDIT.md`
- `.github/agent-pack/DEPLOYMENT_CHECKLIST.md`
- `index.html`
- `robots.txt`
- `sitemap.xml`
- `site.webmanifest`
- `favicon.svg`

No GitHub Secrets, deployment credentials, DNS, Cloudflare settings, production hosting settings, or live production headers were changed or verified.

## Current Architecture

The repository currently serves a static site from the repository root:

- Main document: `index.html`
- Static metadata/assets: `robots.txt`, `sitemap.xml`, `site.webmanifest`, `favicon.svg`
- Deployment: GitHub Actions workflow archives repository root content, excludes `.git`, `.github`, `README.md`, and `AGENTS.md`, then deploys by SSH to an InterServer-style `public_html` target.
- Package manager/framework: none observed in the reviewed repository files.

## Files Reviewed

- `AGENTS.md`: project rules, deployment/security guidance.
- `README.md`: project purpose, deployment expectations, security rules.
- `.github/workflows/deploy.yml`: GitHub Actions deployment workflow and secret references.
- `.github/agent-pack/ISSUE_01_AUDIT.md`: prior deployment and architecture audit context.
- `.github/agent-pack/DEPLOYMENT_CHECKLIST.md`: deployment and verification checklist.
- `index.html`: form behavior, inline script, inline styles, links, generated content, storage/cookie/tracker checks.
- `robots.txt`: crawl policy and sitemap reference.
- `sitemap.xml`: public URL listing.
- `site.webmanifest`: PWA metadata and icon references.
- `favicon.svg`: local SVG favicon content.

## Checks Run

- `pwd`
- `git branch --show-current`
- `git status --short`
- `rg --files`
- `find . -maxdepth 3 -type f`
- `find . -maxdepth 3` package/dependency file check for `package.json`, lockfiles, and `.env` patterns
- Targeted secret scan with `rg -n -i` for private keys, tokens, passwords, API keys, SSH material, `.env`, credentials, and deployment-related terms
- Targeted tracking/storage scan with `rg -n -i` for `localStorage`, `sessionStorage`, `document.cookie`, cookies, IndexedDB, beacon/fetch/XHR, analytics/tracker names, iframes, external embeds, external script tags, and external URLs
- Targeted form scan with `rg -n` for form, mailto, honeypot, inputs, buttons, validation, action, and method markers

## Findings

### No committed secrets found in reviewed files

No private keys, tokens, passwords, API keys, SSH private material, `.env` file content, or deployment credentials were found in the reviewed files.

The only secret-related matches were documentation warnings and GitHub Actions secret references such as `${{ secrets.SSH_PRIVATE_KEY }}`, `${{ secrets.SSH_HOST }}`, `${{ secrets.SSH_USER }}`, and `${{ secrets.SSH_PORT }}`.

### Deployment workflow uses GitHub Secrets rather than committed credentials

`.github/workflows/deploy.yml` keeps deploy credentials in GitHub Secrets and exposes them only inside the deploy job. Repository permissions are limited to `contents: read`.

Noted residual risks:

- `actions/checkout@v4` is version-tagged, not pinned to an immutable SHA.
- `ssh-keyscan` trusts the host key presented during the workflow run instead of checking a pinned expected host key.
- The deploy step deletes existing target contents except `cgi-bin` before extracting the new archive. This is deployment-impacting behavior, but it was pre-existing and not changed for this issue.

### Booking form is mailto-only and honest about client-side behavior

`index.html` booking handling:

- Uses a local form with no `action` and no backend submission.
- Calls `event.preventDefault()` on submit.
- Validates required fields and email shape in client-side JavaScript only.
- Builds a `mailto:` URL addressed to `booking@cyberdjs.org`.
- Opens the user's email client through `window.location.href`.
- States that the page does not store booking details and that the user must review/send the email manually.
- Provides direct `mailto:` links and a `noscript` fallback.

No silent storage or backend collection was found.

### Honeypot remains hidden and safe

The form includes a `website` honeypot field inside `.spam-trap`:

- Positioned off-screen.
- `aria-hidden="true"`.
- `tabindex="-1"`.
- `autocomplete="off"`.
- If filled, the script refuses to prepare the booking email and asks the user to use the direct email link.

### No cookies, web storage, external form provider, trackers, or analytics found

No uses were found for:

- `document.cookie`
- cookies
- `localStorage`
- `sessionStorage`
- IndexedDB
- `fetch`
- `XMLHttpRequest`
- `navigator.sendBeacon`
- external form providers
- analytics/tracking scripts

### No external scripts, iframes, or external embeds found

No `<script src=...>` tags, iframes, tracker scripts, analytics snippets, or live third-party embeds were found.

The page includes inline CSS, inline JavaScript, inline JSON-LD, local metadata assets, `mailto:` links, and public canonical/schema URLs. Music embed data is intentionally placeholder-only and does not load third-party players.

### Dependency audit not applicable

No package files were found in the reviewed repository root scan:

- no `package.json`
- no `package-lock.json`
- no `pnpm-lock.yaml`
- no `yarn.lock`
- no `bun.lockb`

Because this is currently a static no-dependency site, npm/package-manager audit output is not applicable and was not invented.

### Static header hardening added for Apache-style hosting

Added `.htaccess` with conservative headers only:

- `X-Content-Type-Options: nosniff`
- `Referrer-Policy: strict-origin-when-cross-origin`
- `Permissions-Policy: camera=(), microphone=(), geolocation=(), payment=()`
- `X-Frame-Options: SAMEORIGIN`

No Content Security Policy was added because the site currently relies on inline CSS, inline JavaScript, inline JSON-LD, and `mailto:` behavior. A CSP should be added only after accounting for those surfaces explicitly.

Production headers were not live-verified in this review.

## Risks

- GitHub Actions deploy credentials could not be verified without accessing GitHub Secrets, which was intentionally out of scope.
- Live production headers were not checked, so the new `.htaccess` should be verified after deployment.
- The deployment workflow's `ssh-keyscan` approach does not independently verify the expected host identity.
- The workflow deploys the repository root; future local-only files could be published unless deploy include/exclude rules are kept tight.
- The deployment step removes remote target contents except `cgi-bin`; accidental remote-only files in `public_html` could be deleted during deployment.
- Client-side validation improves user feedback but is not a security boundary. This is acceptable because there is no backend collection endpoint.

## Recommendations

1. After deployment, verify live response headers on `https://cyberdjs.org/`.
2. Consider pinning `actions/checkout` to an immutable SHA in a separate CI hardening issue.
3. Consider replacing runtime `ssh-keyscan` trust with a pinned expected host key in a separate deployment hardening issue.
4. Keep the booking form mailto-only unless a future backend issue adds explicit server-side validation, spam controls, retention policy, and privacy documentation.
5. Keep external media players as explicit outbound links unless privacy expectations and consent behavior are reviewed.

## Acceptance Criteria Status

- Check committed files for obvious secrets or accidental sensitive data: passed for reviewed files.
- Review deploy workflow for safe secret usage: passed with residual risks documented.
- Review booking form handling: passed.
- Review external scripts/assets: passed.
- Dependency audit: not applicable; no package files found.
- Headers: conservative Apache `.htaccess` headers added; production headers not live-verified.
- Document scope, files reviewed, checks run, findings, risks, recommendations, and acceptance criteria status: completed.
- Do not claim production headers were verified unless checked live: complied.
- Do not change sitemap, robots, favicon, or manifest without security issue: complied.
- Preserve visual design, SEO, booking behavior, accessibility, and performance: complied.
