# CyberDJs.org

Production website for **CyberDJs**.

## Purpose

CyberDJs.org presents CyberDJs as:

1. **artist crew**
2. **booking destination**
3. **music technology / CyberCore platform**
4. **future community hub**

The site should feel like an underground digital music collective, not a corporate landing page.

## Brand direction

Creative mix:

- dark cyberpunk
- underground hacker culture
- rave energy
- digital brutalism
- experimental music technology
- selective luxury-tech restraint

Reference mood:

**Berlin basement × pirate radio × digital art crew × experimental music lab**

## Repository

Primary branch:

`main`

Production domain:

`https://cyberdjs.org`

Expected deployment:

`main` → GitHub Actions / existing automation → production hosting

Verify the existing deployment workflow before changing it.

## Agent documentation

- `AGENTS.md` — working rules for AI coding agents
- `.github/agent-pack/MASTER_PROMPT.md` — full mission prompt
- `.github/agent-pack/QUICKSTART_FOR_CURSOR_CODEX.md` — short prompt for Cursor / Codex / Claude Code
- `.github/agent-pack/GITHUB_ISSUES.md` — issue breakdown
- `.github/agent-pack/DEPLOYMENT_CHECKLIST.md` — deploy checklist
- `.github/agent-pack/QA_ACCEPTANCE_CHECKLIST.md` — final QA checklist
- `.github/agent-pack/CONTENT_MODEL.md` — suggested data/content model
- `.github/agent-pack/CREATIVE_BRIEF.md` — design and art direction

## Local development

Inspect the repository stack before using commands.

Typical possibilities:

```bash
npm install
npm run dev
npm run build
npm run lint
```

or equivalent package-manager commands depending on the lockfile.

## Site architecture

Recommended production routes:

- `/`
- `/artists`
- `/artists/[artist]`
- `/music`
- `/events`
- `/projects`
- `/booking`
- `/about`

Future routes:

- `/radio`
- `/live`
- `/lab`
- `/releases`
- `/community`

Do not add empty pages.

## Core sections

Homepage should include:

- hero
- crew
- sound/music
- events
- projects/lab
- manifesto
- booking

## Content model

The site should be content/data-driven where practical:

- artists
- mixes
- releases
- events
- projects
- social links
- booking inquiries
- manifesto fragments

## Booking

Booking must be prominent.

Preferred fields:

- name
- email
- organization
- event type
- event date
- location
- message

Protect forms against spam and validate inputs.

## SEO

Implement:

- page titles
- descriptions
- canonical URLs
- OpenGraph metadata
- social preview image
- sitemap
- robots.txt
- favicon set
- structured data

Useful schema:

- `Organization`
- `MusicGroup`
- `Person`
- `MusicEvent`
- `CreativeWork`
- `WebSite`

## Accessibility

Minimum requirements:

- semantic HTML
- keyboard navigation
- visible focus states
- labeled forms
- alt text
- sufficient contrast
- reduced motion support

## Security

Never commit:

- `.env`
- SSH keys
- API tokens
- deployment credentials
- private configuration

## Deployment

Before changing deployment:

1. inspect `.github/workflows`
2. inspect hosting scripts/config
3. verify current production behavior
4. preserve existing working pipeline
5. avoid DNS changes unless required

If DNS is touched, preserve email records:

- MX
- SPF
- DKIM
- DMARC

## Production verification

After deploy, verify:

- homepage
- HTTPS
- mobile layout
- navigation
- assets
- booking flow
- metadata
- sitemap/robots
- 404
- console/network errors
- performance
- accessibility

Production is the source of truth.
