# Issue #14 Production Verification - CyberDJs.org

Date: 2026-08-14

## Scope

Focused production deployment and verification for `https://cyberdjs.org`.

Allowed scope for this issue:

- Verify production deployment behavior.
- Verify production URLs where network access allows.
- Verify local static files and homepage metadata.
- Document what was directly verified and what was not.

No site code, visual design, dependencies, deployment workflow, DNS, Cloudflare settings, analytics, or tracking changes were made.

## Commit / Branch Checked

- Working directory: `/Users/horsedriver/Downloads/cyberdjs.org`
- Branch checked: `codex/issue-14-production-verification`
- Local HEAD checked: `8d0c7a425b4c2d7cc103edcd66b864ee2b7bdc4f`
- Local `main` checked: `8d0c7a425b4c2d7cc103edcd66b864ee2b7bdc4f`

`git fetch origin main` was attempted to refresh the remote `main` reference, but the environment could not resolve `github.com`. Therefore, this report confirms that the checked local branch matches the local `main` commit, but it does not prove that the remote `origin/main` reference was refreshed during this verification session.

## Current Architecture

The current site is a static root-level website:

- Homepage: `index.html`
- Static metadata/assets: `robots.txt`, `sitemap.xml`, `site.webmanifest`, `favicon.svg`
- Apache-style header configuration: `.htaccess`
- Deployment workflow: `.github/workflows/deploy.yml`

The deployment workflow runs on pushes to `main` or manual dispatch, checks out the repository, configures SSH from GitHub Secrets, and deploys repository-root static files to the configured InterServer-style `public_html` target.

No package manager, dependency lockfile, build system, or framework file was found in the repository file list.

## Commands Run

Repository and documentation inspection:

```bash
pwd
git status --short --branch
git status --short
git branch --show-current
git rev-parse HEAD
git rev-parse main
rg --files
sed -n '1,220p' AGENTS.md
sed -n '1,220p' README.md
sed -n '1,220p' .github/workflows/deploy.yml
sed -n '1,260p' .github/agent-pack/DEPLOYMENT_CHECKLIST.md
sed -n '1,260p' .github/agent-pack/QA_ACCEPTANCE_CHECKLIST.md
sed -n '1,260p' .github/agent-pack/ISSUE_13_SECURITY_REVIEW.md
sed -n '1,260p' index.html
sed -n '1,220p' robots.txt
sed -n '1,220p' sitemap.xml
sed -n '1,220p' site.webmanifest
sed -n '1,220p' .htaccess
find .github -maxdepth 3 -type f
```

Targeted local static checks:

```bash
rg -n "<(title|meta|link|script)|property=\"og:|name=\"twitter:|application/ld\\+json|rel=\"canonical\"" index.html
rg -n "href=\"#|id=\"|mailto:|bookingForm|localStorage|sessionStorage|document\\.cookie|cookie|iframe|<script src|analytics|gtag|googletagmanager|plausible|fathom|posthog|fetch\\(|XMLHttpRequest|sendBeacon" index.html
rg -n "package.json|package-lock.json|pnpm-lock.yaml|yarn.lock|bun.lockb" -g "*" .
```

Production and remote checks:

```bash
curl -I https://cyberdjs.org/
git fetch origin main
curl --http1.1 --max-time 15 -I https://cyberdjs.org/
curl --http1.1 --max-time 15 -I https://cyberdjs.org/robots.txt
curl --http1.1 --max-time 15 -I https://cyberdjs.org/sitemap.xml
curl --http1.1 --max-time 15 -I https://cyberdjs.org/favicon.svg
curl --http1.1 --max-time 15 -I https://cyberdjs.org/site.webmanifest
curl --http1.1 --max-time 20 -I https://cyberdjs.org/
curl --http1.1 --max-time 20 -I https://cyberdjs.org/robots.txt
curl --http1.1 --max-time 20 -I https://cyberdjs.org/sitemap.xml
curl --http1.1 --max-time 20 -I https://cyberdjs.org/favicon.svg
curl --http1.1 --max-time 20 -I https://cyberdjs.org/site.webmanifest
```

Local static server attempt:

```bash
python3 -m http.server 8765
curl --max-time 5 -I http://127.0.0.1:8765/
curl --max-time 5 -I http://127.0.0.1:8765/robots.txt
curl --max-time 5 -I http://127.0.0.1:8765/sitemap.xml
curl --max-time 5 -I http://127.0.0.1:8765/favicon.svg
curl --max-time 5 -I http://127.0.0.1:8765/site.webmanifest
curl -g --max-time 5 -I 'http://[::1]:8765/'
curl -g --max-time 5 -I 'http://[::1]:8765/robots.txt'
curl -g --max-time 5 -I 'http://[::1]:8765/sitemap.xml'
curl -g --max-time 5 -I 'http://[::1]:8765/favicon.svg'
curl -g --max-time 5 -I 'http://[::1]:8765/site.webmanifest'
```

## Production Checks

### Production URL Responses

Manual terminal evidence pasted after the original report verified the required production URLs over HTTPS with HTTP/1.1:

- `https://cyberdjs.org/` returned `HTTP/1.1 200 OK`
- `https://cyberdjs.org/robots.txt` returned `HTTP/1.1 200 OK`
- `https://cyberdjs.org/sitemap.xml` returned `HTTP/1.1 200 OK`
- `https://cyberdjs.org/favicon.svg` returned `HTTP/1.1 200 OK`
- `https://cyberdjs.org/site.webmanifest` returned `HTTP/1.1 200 OK`

Observed homepage response details from the original successful production check:

- Status: `HTTP/2 200`
- HTTPS: working for the checked request
- `content-type: text/html`
- `last-modified: Fri, 14 Aug 2026 09:33:05 GMT`
- `server: cloudflare`
- `strict-transport-security: max-age=31536000; includeSubDomains; preload`
- `x-content-type-options: nosniff`
- `referrer-policy: strict-origin-when-cross-origin`
- `permissions-policy: camera=(), microphone=(), geolocation=(), payment=()`
- `x-frame-options: SAMEORIGIN`
- `x-turbo-charged-by: LiteSpeed`

The live production responses confirm that HTTPS works for the checked URLs and that the `.htaccess` hardening headers from Issue #13 are present on the production homepage response.

Non-critical follow-up note:

- `site.webmanifest` returned `200 OK`, but its `Content-Type` was `application/octet-stream`; consider setting a more specific MIME type later if PWA/install behavior matters.

Earlier bounded `curl --http1.1 --max-time` checks from the Codex execution environment timed out with `curl: (28) Connection timed out`, and earlier TLS attempts also failed intermittently with `curl: (35) LibreSSL SSL_connect: SSL_ERROR_SYSCALL`. Those failures are retained as verification-environment/network limitations and are superseded for the production URL status by the successful manual terminal evidence.

### Production Security Headers

The expected production security headers were observed:

- `strict-transport-security`
- `x-content-type-options`
- `referrer-policy`
- `permissions-policy`
- `x-frame-options`

### Latest Main Deployment

Evidence supporting deployment freshness:

- Local `main` and the checked branch both point to `8d0c7a425b4c2d7cc103edcd66b864ee2b7bdc4f`.
- Production homepage returned `last-modified: Fri, 14 Aug 2026 09:33:05 GMT`.
- Production homepage included the `.htaccess` headers expected from the current repository state.

Limitation:

- `git fetch origin main` failed with `Could not resolve host: github.com`, so this session could not refresh and prove the latest remote `origin/main` commit.
- Full byte-for-byte production body comparison against local `index.html` was not completed.
- Live `curl`/`grep` did verify deployed homepage metadata, JSON-LD and booking contact markers.

Status: verified with documented limitations. The production site is live, required production URLs return `200 OK`, HTTPS works, expected headers are present, and live metadata is present. Remote `origin/main` refresh and full byte-for-byte body equality were not completed in this environment.

## Local Checks

### Homepage Metadata

Verified on the live homepage by `curl`/`grep`:

- Title exists: `CyberDJs - Underground Artist Crew, Booking Signal and Music Lab`
- Meta description exists and includes booking contact context.
- Canonical exists: `https://cyberdjs.org/`
- OpenGraph tags exist:
  - `og:type`
  - `og:url`
  - `og:title`
  - `og:description`
  - `og:site_name`
  - `og:locale`
- Twitter tags exist:
  - `twitter:card`
  - `twitter:title`
  - `twitter:description`
- JSON-LD exists via `<script type="application/ld+json">`.
- Booking contact `booking@cyberdjs.org` exists.

### Navigation Anchor Targets

Verified local anchor links and matching IDs in `index.html`:

- `#top` -> `<body id="top">`
- `#main-content` -> `<main id="main-content">`
- `#crew` -> `<section id="crew">`
- `#sound` -> `<section id="sound">`
- `#events` -> `<section id="events">`
- `#lab` -> `<section id="lab">`

The booking section has `<section id="booking">`. Current visible navigation uses direct booking `mailto:` links rather than a `#booking` navigation link.

### Booking Mailto Form Logic

Verified in `index.html`:

- Booking form exists: `id="booking-form"`.
- Required fields and inline error targets are present for name, email, event type, and message.
- Honeypot field exists: `name="website"`, `tabindex="-1"`, `autocomplete="off"`.
- JavaScript submit handler is present.
- Submit handler prevents default form submission.
- Booking email is built as `mailto:booking@cyberdjs.org`.
- `noscript` fallback provides direct email instructions.
- Direct booking `mailto:` links are present in header/hero/booking/footer areas.

### External Scripts, Embeds, Tracking, Storage

Verified by targeted scan of `index.html`:

- No `<script src=...>` external scripts found.
- No iframes found.
- No analytics/tracker markers found for common snippets such as `gtag`, `googletagmanager`, `plausible`, `fathom`, or `posthog`.
- No `localStorage`.
- No `sessionStorage`.
- No `document.cookie`.
- No `fetch(`.
- No `XMLHttpRequest`.
- No `navigator.sendBeacon`.

The only scripts found are inline JSON-LD and inline site behavior JavaScript.

### Local Static Server

Attempted:

- `python3 -m http.server 8765`
- bounded curl checks against `127.0.0.1:8765`
- bounded curl checks against `[::1]:8765`

The Python server reported:

```text
Serving HTTP on :: port 8765 (http://[::]:8765/) ...
```

However, curl could not connect to either `127.0.0.1:8765` or `[::1]:8765` from this execution environment. Local static serving was attempted but not verified by HTTP response.

## Findings

- Production homepage and required static production URLs returned `HTTP/1.1 200 OK` over HTTPS in manual terminal evidence.
- Production homepage emitted the expected `.htaccess` security headers:
  - `strict-transport-security`
  - `x-content-type-options`
  - `referrer-policy`
  - `permissions-policy`
  - `x-frame-options`
- Live homepage metadata, canonical, OpenGraph/Twitter tags, JSON-LD, and `booking@cyberdjs.org` were verified by `curl`/`grep`.
- Local navigation anchor targets checked by source inspection are present.
- Booking mailto form logic remains present.
- No external scripts, iframes, analytics, trackers, cookies, localStorage, or sessionStorage were found in the local homepage source.
- No package manager or lockfile was found, so install/build/lint/package audit checks are not applicable for the current static site shape.

## Remaining Risks

- Remote `origin/main` could not be refreshed because GitHub DNS failed in this environment.
- Full byte-for-byte production body equality against local `index.html` was not verified. Live metadata and booking markers were verified instead.
- Earlier required production asset URL checks from inside the Codex execution environment timed out, but later manual terminal evidence verified those production URLs as `HTTP/1.1 200 OK`.
- Browser rendering, mobile layout, production console, production network panel, accessibility tooling, and Lighthouse were not performed and are not claimed.
- Local static server HTTP responses were not verified because local curl could not connect to the Python server in this environment.
- Cloudflare/DNS/GitHub Secrets/GitHub Actions run status were not inspected or changed.
- `site.webmanifest` returned `200 OK` but used `Content-Type: application/octet-stream`; this is non-critical unless PWA/install behavior matters.

## Acceptance Criteria Status

- Confirm latest main is deployed: verified with documented limitations; local `main` equals checked HEAD and production headers/metadata match the current repo state, but remote `origin/main` refresh and full byte-for-byte body equality were blocked by network limitations.
- Check `https://cyberdjs.org/`: verified with `HTTP/1.1 200 OK` over HTTPS.
- Check `https://cyberdjs.org/robots.txt`: verified with `HTTP/1.1 200 OK` over HTTPS.
- Check `https://cyberdjs.org/sitemap.xml`: verified with `HTTP/1.1 200 OK` over HTTPS.
- Check `https://cyberdjs.org/favicon.svg`: verified with `HTTP/1.1 200 OK` over HTTPS.
- Check `https://cyberdjs.org/site.webmanifest`: verified with `HTTP/1.1 200 OK` over HTTPS.
- Check HTTPS works: verified for homepage and required static production URLs.
- Check production assets: verified; required static production URLs returned `HTTP/1.1 200 OK` over HTTPS.
- Check response headers including `.htaccess` headers: verified for expected production security headers.
- Check homepage HTML metadata: verified on the live homepage by `curl`/`grep`.
- Check navigation anchor targets exist: passed by local source inspection.
- Check booking mailto form logic remains present: passed by local source inspection.
- Check no external scripts, iframes, analytics, trackers, cookies, localStorage/sessionStorage: passed by local source inspection.
- Run local static server if useful: attempted; server started, but curl could not connect in this environment.
- Document what was directly verified and what was not: verified.
- Do not claim browser/mobile/console checks unless actually performed: complied.
- Do not invent Lighthouse scores: complied.
- Remaining issues known and non-critical: yes; remaining items are verification-environment limitations, not confirmed production blockers.
