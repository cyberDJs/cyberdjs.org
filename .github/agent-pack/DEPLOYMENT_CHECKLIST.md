# Deployment Checklist — CyberDJs.org

Use before and after deploying `cyberdjs.org`.

## 1. Preflight

- [ ] Inspect repository tree
- [ ] Inspect package manager and lockfile
- [ ] Inspect `.github/workflows`
- [ ] Confirm deployment branch is `main`
- [ ] Confirm required GitHub secrets exist
- [ ] Confirm target hosting path
- [ ] Confirm current production site behavior
- [ ] Confirm no secrets are committed

## 2. Build

- [ ] Install dependencies
- [ ] Run local dev server
- [ ] Run build command
- [ ] Run lint/typecheck if available
- [ ] Fix critical warnings/errors

## 3. Deployment pipeline

Expected path:

`main` → GitHub Actions → InterServer / hosting → `https://cyberdjs.org`

- [ ] Reuse existing workflow if it works
- [ ] Do not redesign deployment without cause
- [ ] Do not touch DNS unless required
- [ ] Preserve mail records if DNS is touched

Required mail records to protect:

- MX
- SPF
- DKIM
- DMARC
- mail host records

## 4. Production verification

- [ ] `https://cyberdjs.org` loads
- [ ] HTTPS works
- [ ] homepage loads cleanly
- [ ] navigation works
- [ ] mobile layout works
- [ ] assets load
- [ ] booking path works
- [ ] 404 works
- [ ] console checked
- [ ] network errors checked
- [ ] metadata checked
- [ ] sitemap/robots checked if present
- [ ] performance reviewed
- [ ] accessibility reviewed

## 5. Final report

Include:

- live URL
- stack
- deployment behavior
- important commits/PRs
- QA result
- remaining owner decisions
