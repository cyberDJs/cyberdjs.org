# Issue #1 Audit — CyberDJs.org

Scope: limited repository audit for GitHub Issue #1.

This audit is based only on the files explicitly allowed for inspection:

- `AGENTS.md`
- `README.md`
- `.github/agent-pack/MASTER_PROMPT.md`
- `.github/agent-pack/DEPLOYMENT_CHECKLIST.md`
- `.github/workflows/deploy.yml`
- `index.html`

No build, full repository scan, production code change, deployment workflow edit, or live production verification was performed.

## 1. Repo structure

Observed or documented structure from the allowed files:

```text
.
├── AGENTS.md
├── README.md
├── index.html
└── .github/
    ├── workflows/
    │   └── deploy.yml
    └── agent-pack/
        ├── MASTER_PROMPT.md
        ├── DEPLOYMENT_CHECKLIST.md
        ├── QUICKSTART_FOR_CURSOR_CODEX.md
        ├── GITHUB_ISSUES.md
        ├── QA_ACCEPTANCE_CHECKLIST.md
        ├── CONTENT_MODEL.md
        └── CREATIVE_BRIEF.md
```

Only the files listed in the scope were opened. The additional `agent-pack` files above are referenced by `README.md`, but were not inspected.

## 2. Current stack

Current implementation appears to be a static website:

- Entry point: `index.html`
- Language/runtime observed: HTML only
- Framework observed: none
- Package manager observed: none from allowed files
- Build system observed: none from allowed files
- Database observed: none
- Backend observed: none

`README.md` says agents should inspect the repository stack before using commands and lists typical possible npm commands, but no package manager or lockfile was confirmed in this scoped audit.

## 3. Deploy workflow summary

`.github/workflows/deploy.yml` defines a GitHub Actions workflow named `Deploy to InterServer`.

Trigger:

- Pushes to `main`
- Manual `workflow_dispatch`

Permissions:

- `contents: read`

Main job behavior:

- Runs on `ubuntu-latest`
- Checks out repository with `actions/checkout@v4`
- Configures SSH using GitHub secrets:
  - `SSH_PRIVATE_KEY`
  - `SSH_PORT`
  - `SSH_HOST`
  - `SSH_USER`
- Adds host key with `ssh-keyscan`
- Creates a tar archive of the repository while excluding:
  - `.git`
  - `.github`
  - `README.md`
  - `AGENTS.md`
- SSHes to hosting
- Creates target directory if needed
- Removes existing target contents except `cgi-bin`
- Extracts the archive into the target directory

## 4. Hosting target

The deployment workflow targets InterServer-style shared hosting.

Configured target path:

```text
/home/eimyherr/domains/cyberdjs.org/public_html
```

Documented production domain:

```text
https://cyberdjs.org
```

Expected deployment path from project docs:

```text
main → GitHub Actions → InterServer / hosting → https://cyberdjs.org
```

This audit did not verify the live production site.

## 5. Risks

- The current `index.html` is a minimal placeholder stating that GitHub deploy is working; it does not yet meet the documented product, brand, SEO, accessibility, booking, or content goals.
- No package manager, framework, tests, linting, build, sitemap, robots file, or asset pipeline was confirmed from the allowed files.
- The deploy workflow deletes existing files in the hosting target except `cgi-bin` before extracting the new archive. This may be intended, but it is high impact if unexpected files exist in `public_html`.
- Deployment depends on GitHub repository secrets that were not verified in this audit.
- `ssh-keyscan` records the presented host key during the workflow. This is common but does not independently verify the expected host identity.
- The workflow deploys the repository root contents directly. Future source files, drafts, or local-only artifacts could be published unless excluded or moved out of the deploy payload.
- Production behavior, HTTPS, DNS, mail records, mobile layout, metadata, console errors, and accessibility were not checked in this scoped audit.

## 6. Recommended next steps

1. Confirm Issue #1 acceptance criteria against this audit and close it only if documentation-level discovery is sufficient.
2. In a separate implementation issue, inspect the package manager/lockfile and broader repository structure before choosing whether to keep the site static or introduce a framework.
3. Preserve the existing deploy workflow unless a verified deployment problem requires a targeted fix.
4. Add a production-ready homepage in a focused branch, with booking visibility, semantic HTML, metadata, responsive layout, and reduced-motion support.
5. Add deployment payload safeguards before the site grows, such as an explicit publish directory or stricter archive include list.
6. Verify required GitHub secrets and the live `https://cyberdjs.org` deployment path before any production release claim.

## 7. Can Issue #1 be closed?

Yes, if Issue #1 is limited to creating a scoped repository/deployment audit document.

No, if Issue #1 requires live production verification, full repository inspection, build/test execution, or implementation work. Those activities were explicitly out of scope for this pass.
