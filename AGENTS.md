# AGENTS.md — CyberDJs.org

Instructions for AI coding agents working in this repository.

## Project

Production website for:

**CyberDJs**  
**https://cyberdjs.org**

Repository:

**cyberDJs/cyberdjs.org**

Primary branch:

**main**

## Core goal

Build and maintain a production-grade website that presents CyberDJs as:

1. artist crew
2. booking destination
3. CyberCore-connected music technology platform
4. future community hub

The primary identity is **artist crew**.

## Working rules

Before changing code:

1. inspect repository structure
2. inspect package manager and lockfile
3. inspect current README
4. inspect `.github/workflows`
5. inspect existing deployment scripts
6. inspect existing assets
7. inspect current production site if possible

Preserve useful work.

Do not rewrite infrastructure without cause.

## Deployment rule

Assume the current pipeline may already be:

`main` → GitHub Actions → hosting → `cyberdjs.org`

Verify before changing.

If it works, reuse it.

If it fails, fix the smallest necessary part.

Do not touch Cloudflare or DNS unless required.

If DNS is touched, preserve mail records:

- MX
- SPF
- DKIM
- DMARC
- mail host records

## Security

Never commit:

- `.env`
- SSH keys
- API tokens
- deployment secrets
- private config
- credentials in docs

Check staged files before commit.

Use environment variables for secrets.

Validate form inputs.

Avoid unnecessary third-party scripts.

## Design rules

The site must feel like:

**Berlin basement × pirate radio × digital art crew × experimental music lab**

Use:

- dark base
- strong typography
- restrained neon
- waveform / frequency / signal motifs
- purposeful motion
- brutalist layout moments
- clean high-end spacing where useful

Avoid:

- generic Matrix code
- stock DJ images
- fake terminals
- excessive neon gradients
- template landing page layout
- meaningless glitch effects
- crypto/startup clichés

## UX rules

Mobile is first-class.

Booking must be visible.

Navigation must be simple.

Audio must not autoplay.

Respect `prefers-reduced-motion`.

Use semantic HTML.

Use visible focus states.

## Content rules

No lorem ipsum.

Use provisional content only when necessary.

Mark owner-verification content clearly in data/comments.

Keep copy short, sharp and specific.

Avoid generic AI marketing language.

## Recommended data models

Keep content data-driven where practical:

- artists
- mixes/releases
- events
- projects
- social links
- booking contacts
- manifesto fragments

New artists/projects/events should be addable without rewriting page logic.

## Suggested components

Use reusable components:

- `Navigation`
- `Footer`
- `SectionHeader`
- `BookingCTA`
- `ArtistCard`
- `EventCard`
- `ProjectCard`
- `MediaEmbed`
- `WaveformVisual`
- `GlitchText`
- `ManifestoBlock`
- `StatusPill`

## Quality gates

Before merge/deploy:

- install succeeds
- build succeeds
- lint/typecheck succeeds if available
- homepage renders
- mobile layout checked
- navigation checked
- booking flow checked
- no secrets committed
- console checked
- metadata checked
- sitemap/robots checked where applicable
- accessibility reviewed
- performance reviewed

## Commit style

Use logical commits:

- `feat: build CyberDJs homepage experience`
- `feat: add artist data model`
- `feat: implement booking flow`
- `feat: add projects lab section`
- `seo: add metadata and structured data`
- `perf: optimize assets and motion`
- `fix: repair deployment workflow`
- `docs: document deployment process`

## Definition of done

A task is done only when it is implemented, tested, documented if necessary and does not damage production deployment.

The whole mission is done only when `https://cyberdjs.org` is live and directly verified.
