# Issue #2 — Information Architecture and Content Model

Scope: concise planning document for GitHub Issue #2.

This document is based only on:

- `AGENTS.md`
- `README.md`
- `.github/agent-pack/MASTER_PROMPT.md`
- `.github/agent-pack/CONTENT_MODEL.md`
- `.github/agent-pack/CREATIVE_BRIEF.md`
- `.github/agent-pack/ISSUE_01_AUDIT.md`
- `index.html`

No build, production code change, deployment workflow edit, broader repository scan, or live production verification was performed.

## 1. Final recommended site routes

Initial production routes:

- `/` — homepage and primary narrative
- `/artists` — crew overview
- `/artists/[artist]` — individual artist profile, only when verified artist data exists
- `/music` — mixes, releases, playlists, videos
- `/events` — upcoming and past appearances
- `/projects` — CyberCore-connected tools, experiments, and lab work
- `/booking` — booking inquiry path and contact requirements
- `/about` — crew context, manifesto, and platform direction

Future routes, not for the first implementation unless real content exists:

- `/radio`
- `/live`
- `/lab`
- `/releases`
- `/community`

Rule: do not create empty pages. If a route lacks real or explicitly provisional content, surface that content on the homepage or hide the route until ready.

## 2. Homepage narrative

The homepage should present CyberDJs first as an artist crew, then as a booking destination, then as a music-technology platform.

Recommended sequence:

1. Hero: strong CyberDJs identity, short positioning line, visible booking CTA.
2. Crew: featured artists and sound identities.
3. Sound: current mixes, releases, playlists, or videos without autoplay.
4. Events: next confirmed appearances, then recent past events if no upcoming dates exist.
5. Projects/lab: CyberCore, dumpAmp, DJ tools, AI-assisted workflows, and experimental systems.
6. Manifesto: short fragments that communicate underground culture, human taste, and machine-assisted practice.
7. Booking CTA: repeated clear path for clubs, festivals, private events, collaborations, and platform inquiries.

Tone: sharp, minimal, specific, human. Avoid generic AI marketing copy, stock DJ framing, fake terminals, Matrix code, and meaningless glitch effects.

## 3. Content model for artists

Recommended fields:

- `id`: stable slug
- `name`: public artist name
- `role`: DJ, producer, visual artist, technologist, resident, guest, or collaborator
- `shortBio`: concise verified bio
- `genres`: list of sound/style tags
- `location`: optional city or region
- `image`: optional portrait, press image, or abstract identity asset
- `links.website`
- `links.soundcloud`
- `links.spotify`
- `links.instagram`
- `links.youtube`
- `links.mixcloud`
- `links.booking`
- `featuredMixIds`: related music items
- `status`: `active`, `guest`, `alumni`, or `hidden`
- `ownerVerified`: boolean

Artist pages should not publish unverified biographies, claims, press quotes, residencies, or social links.

## 4. Content model for events

Recommended fields:

- `id`: stable slug
- `title`: public event title
- `date`: ISO date
- `time`: optional local start time
- `city`
- `country`
- `venue`
- `artistIds`: linked CyberDJs artists
- `url`: official ticket, event, or venue URL
- `status`: `upcoming`, `past`, `cancelled`, or `draft`
- `eventType`: club night, festival, private event, stream, workshop, lab session, or collaboration
- `description`: short public copy
- `ageRestriction`: optional
- `image`: optional flyer or event image
- `ownerVerified`: boolean

Past events can support credibility, but upcoming events should be prioritized. Cancelled events should be hidden by default unless there is a clear user need to show them.

## 5. Content model for music, mixes, and releases

Recommended fields:

- `id`: stable slug
- `title`
- `artistIds`
- `type`: `mix`, `release`, `playlist`, or `video`
- `platform`: `soundcloud`, `spotify`, `apple`, `youtube`, `mixcloud`, or `other`
- `url`: canonical external URL
- `embedUrl`: optional embed URL
- `date`: release or publication date
- `description`: short context
- `genres`: optional sound tags
- `duration`: optional runtime
- `coverImage`: optional artwork
- `explicit`: optional boolean
- `ownerVerified`: boolean

Audio and video must not autoplay. If embeds are unavailable or privacy-sensitive, link out with a clear platform label instead of loading third-party players by default.

## 6. Content model for projects/lab

Recommended fields:

- `id`: stable slug
- `title`
- `tagline`
- `description`
- `status`: `idea`, `prototype`, `active`, `archived`, or `hidden`
- `tags`: music tech, CyberCore, DJ tools, AI workflow, visual system, research, community
- `links.repo`
- `links.demo`
- `links.docs`
- `links.caseStudy`
- `featured`: boolean
- `ownerVerified`: boolean

Projects should make CyberDJs feel like an experimental music lab, but claims about CyberCore integration, public availability, open source status, or technical capability must be owner-verified before launch.

## 7. Booking/contact content requirements

Booking must be visible from the homepage and navigation.

Required inquiry fields:

- name
- email
- organization
- event type
- event date
- location
- message

Recommended optional fields:

- expected audience size
- budget range
- preferred artist or format
- phone
- website or event link

Required content:

- booking email or verified form destination
- expected response time, if known
- bookable formats: club, festival, private event, stream, workshop, collaboration, or lab/demo
- location/travel availability, if known
- privacy note for inquiry handling

Implementation notes for later issues: validate input, protect against spam, label form controls, and avoid committing secrets or private routing details.

## 8. Provisional content fields needing owner verification

The following must be marked as provisional until Jan verifies them:

- artist names, aliases, roles, biographies, locations, and images
- artist social/music links
- genres and sound descriptions
- event titles, dates, venues, ticket links, and status
- release/mix titles, dates, platform URLs, embeds, and artwork
- CyberCore, dumpAmp, AI workflow, and lab capability claims
- public booking email or form destination
- bookable formats, rates, travel range, and response time
- manifesto copy intended as final brand voice
- SEO descriptions, OpenGraph copy, and structured data facts

Provisional fields should use short comments or metadata such as `ownerVerified: false`; they should not be disguised as confirmed production facts.

## 9. Empty-state rules

- Do not create route-level dead ends.
- Hide empty sections when no content exists and there is no useful fallback.
- For artists, show only verified artists or clearly marked provisional profile cards during internal review.
- For events, show upcoming events first; if none exist, show recent past events; if no event data exists, omit the section except for booking.
- For music, prefer one verified link over several placeholder embeds.
- For projects, show active/prototype work first; hide `idea` items unless they are part of the public narrative.
- For booking, never hide the CTA; if no form exists, use a verified email fallback.
- Empty copy should be specific, not generic. Avoid "coming soon" unless a real launch path exists.

## 10. Can Issue #2 be closed?

Yes, if Issue #2 is limited to defining the information architecture and content model in this planning document.

No, if Issue #2 requires implementation, route creation, production content entry, owner verification, build/test execution, or live production verification. Those activities belong to later issues.
