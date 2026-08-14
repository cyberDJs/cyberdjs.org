# Issue #34 — Verified CyberDJs Content Inventory

## Purpose and handling

This is an intake and publishing plan, not a source of public claims. The current homepage is a static, data-driven single page whose crew, music, event, and lab records are explicitly provisional. Replace a placeholder only after the relevant owner and subject have confirmed the public-facing data.

Use one verification status on every record and public-facing asset:

- `ready` — owner verified, permission confirmed where needed, and safe to publish.
- `needs review` — supplied, but an owner, artist, venue, rights holder, or link owner must still confirm it.
- `missing` — no usable data or asset has been supplied.
- `do not publish yet` — private, embargoed, uncertain, expired, or not approved for public use.

## 1. Current website content areas

| Area | Current content shape | Inventory action |
| --- | --- | --- |
| Header / navigation | CyberDJs wordmark and icon; links to Crew, Sound, Events, Lab; booking CTA. | Confirm public navigation labels, final logo use, and booking destination. |
| Hero | CyberDJs identity, positioning copy, booking and sound CTAs, decorative signal visual. | Confirm final positioning and whether any location, roster, or availability statement is public. |
| Crew / artists | Three generic, explicitly provisional roster cards: resident signal, pirate radio operator, and lab collaborator. | Collect verified individual profiles before publishing names, roles, bios, locations, tags, links, or portraits. |
| Music / sound | Two provisional slots for a mix and a release, with no working public links or embeds. | Collect one verified item at a time: canonical link, platform, artist credit, date, artwork rights, and embed preference. |
| Events | Empty upcoming state plus two archived-format placeholders. | Collect confirmed public listings and separately verify historic appearances before publishing. |
| Lab / projects | Provisional CyberCore workflows, dumpAmp direction, and visual-systems lab descriptions. | Confirm public project names, descriptions, relationships, status, links, screenshots, and capability claims. |
| Booking | Public `booking@cyberdjs.org` mailto/email-draft flow for events and collaborations. | Confirm inbox ownership, public booking scope, response expectations, travel/rate policy, and which routing details stay private. |
| Footer / contact / social | Short crew description, section links, and booking email; no social profile links. | Confirm footer copy, public contact details, location wording, and official social/profile URLs. |
| Media / logo / photos | Approved header icon exists; no verified artist photography, event imagery, or social-preview asset is identified here. | Gather approved logo derivatives and consented, rights-cleared media with accompanying metadata. |

## 2. Placeholder and replacement map

| Section | Current placeholder-like content | Real data needed | Verify before publishing | Keep internal / private |
| --- | --- | --- | --- | --- |
| Header / hero | Generic positioning; “Booking is open”; “Crew roster opening soon.” | Final approved positioning, roster availability, booking availability. | Owner approval of every claim and booking status. | Unannounced roster, launch timing, internal strategy. |
| Crew | Generic roles, bios, genre tags, and `Location TBA`. | Public name/alias, role, approved bio, styles, city/base, links, photo. | Artist approval, correct URLs, image rights, and whether city is public. | Legal name, home address, private identity, personal contact details, unreleased plans. |
| Music | “Basement transmission 001,” “Signal archive,” TBA dates/duration, placeholder player. | Title, credited artists, type, platform URL, date, duration, description, artwork. | Rights/ownership, canonical URL, credits, release date, embed/privacy preference. | Private masters, unreleased tracks, distributor data, draft links, royalties. |
| Events | “Club night format,” “Lab session format,” TBA city/venue. | Event title, date/time/timezone, venue, city, lineup, official URL, image, status. | Venue/promoter confirmation, date/status, artist participation, ticket URL, image rights. | Holds, contracts, fees, guest lists, travel plans, private venue contacts. |
| Lab / projects | Broad CyberCore, dumpAmp, and visual-lab descriptions. | Public name, concise description, current public status, crew relation, tags, approved links/media. | Owner approval of technical capability, public availability, relationship, repository/demo access. | Architecture, security details, private repos, roadmap, credentials, client work. |
| Booking | Public email and broad format list. | Approved inbox, formats, territory/travel policy, response expectation, optional booking brief. | Inbox owner and consent, scope, privacy wording, current availability. | Rates, contracts, direct phone numbers, routing aliases, personal calendars. |
| Footer / social | “Prague / Berlin frequency” and no profile links. | Approved location wording, official profile URLs, contact labels. | Account ownership, handle spelling, profile visibility, brand approval. | Personal accounts, recovery addresses, account access details. |
| Media | Logo use is defined; artist/event imagery is absent. | Approved files, captions, alt text, creator/source, licence, consent, crop guidance. | Rights holder and subject consent, allowed channels/crops, accurate caption, accessibility text. | Raw shoots, EXIF-sensitive originals, contracts, release forms, private backstage imagery. |

## 3. Reusable content schema

Every record needs `id`, `verificationStatus`, `verifiedBy`, `verifiedAt`, `publicNotes`, and `privateNotes`. Store private notes outside public site data.

### Artists / DJs / members

`id`, `publicName`, `role`, `shortBio`, `longBio`, `genres`, `cityBase`, `bookingPreferences`, `profilePhotoId`, `logoOrAvatarId`, `socialLinkIds`, `musicItemIds`, `eventIds`, `projectIds`, `publicVisibility`, `consentConfirmed`.

### Music links / releases / sets

`id`, `title`, `artistIds`, `type`, `platform`, `canonicalUrl`, `embedUrl` (optional), `publishedDate`, `duration`, `description`, `genres`, `coverMediaId`, `credits`, `explicit`, `publicVisibility`, `rightsConfirmed`.

### Events

`id`, `title`, `startDateTime`, `timezone`, `city`, `country`, `venue`, `eventType`, `artistIds`, `officialUrl`, `ticketUrl`, `status`, `description`, `eventMediaId`, `ageRestriction`, `publicVisibility`, `promoterConfirmed`.

### Lab / projects

`id`, `title`, `tagline`, `description`, `status`, `tags`, `crewRelation`, `linkIds`, `mediaIds`, `publicAvailability`, `publicVisibility`, `claimApprovalConfirmed`.

### Booking / contact

`id`, `label`, `publicEmail`, `formDestination` (if introduced later), `bookableFormats`, `serviceArea`, `responseExpectation`, `privacyNote`, `publicVisibility`, `inboxOwnerConfirmed`.

### Social / profile links

`id`, `ownerType`, `ownerId`, `platform`, `label`, `url`, `official`, `publicVisibility`, `linkOwnerConfirmed`.

### Photos / media

`id`, `fileName`, `mediaType`, `subject`, `creator`, `sourceUrl` (optional), `licenceOrPermission`, `consentConfirmed`, `allowedUses`, `cropNotes`, `altText`, `caption`, `dimensions`, `aspectRatio`, `publicVisibility`, `optimizationComplete`.

## 4. Artist / DJ intake checklist

Each member, including Eimy, should complete this checklist and mark each answer with a verification status.

- Public artist name / alias and exact capitalization.
- Preferred role or title (for example DJ, producer, selector, visual artist, technologist, collaborator).
- Short public bio (one to two sentences) and optional longer public bio.
- Genres, styles, and sound descriptors the artist approves.
- Public city/base, or explicit confirmation that location should be omitted.
- Booking preferences: solo/crew formats, preferred event types, public travel or availability wording, and any limits.
- Press-photo requirement: preferred image, photographer credit, approved crops, and expiration/review date if applicable.
- Logo/avatar requirement: approved asset or confirmation to use text-only presentation.
- Official public social/profile links and music links, with owner confirmation for each URL.
- Verified public event history: title, venue, city, date, official link, and permission to list it.
- Public projects/lab involvement, wording of contribution, and approved links/media.
- Explicit public-versus-private split: what may appear on the site, what is booking-only, and what must never be published.
- Permission/consent confirmation for bio, name, image, links, event history, and project attribution; record who confirmed and when.

## 5. Media requirements

### File names and folders

- Use lowercase ASCII names with hyphens: `artist-public-name-press-01.jpg`, `event-slug-flyer-2026-10-24.jpg`.
- Use stable folders by purpose: `assets/brand/`, `assets/artists/<artist-id>/`, `assets/events/<event-id>/`, `assets/projects/<project-id>/`.
- Keep source/master files separate from optimized web derivatives; do not overwrite an approved master.

### Dimensions and presentation

| Use | Aspect ratio | Recommended delivered size |
| --- | --- | --- |
| Artist portrait | 1:1 or 4:5 | at least 1600 px on the long edge |
| Event flyer | original ratio; provide a 4:5 crop if appropriate | at least 1600 px on the long edge |
| Project/editorial image | 16:9 or 3:2 | at least 1920 px wide |
| Logo / mark | vector preferred; square fallback for icon use | SVG where available; otherwise at least 512 px square PNG |

- Provide concise, factual alt text that identifies meaningful content; use empty alt text only for a purely decorative duplicate.
- Record creator, source, licence/permission, subject consent, permitted placement, caption, and crop restrictions with every file.
- Optimize copies for web delivery, preserve an appropriate format, remove unnecessary metadata, and test legibility at mobile sizes.
- Do not upload unlicensed or unconsented media, stock images posing as crew imagery, private originals, raw files containing sensitive metadata, screenshots with private information, or assets whose creator/source is unknown.

## 6. Publishing rules

- Do not publish unverified claims.
- Do not publish private contacts, booking operations, contracts, rates, calendars, access details, or personal data.
- Do not invent artist, event, project, location, release, credit, or performance data.
- Prefer an empty or specific coming-soon state over fake content.
- Publish only `ready` records. Leave `needs review`, `missing`, and `do not publish yet` out of public content unless an owner explicitly approves a clearly labelled internal-preview use.
- Recheck time-sensitive records (event dates, ticket links, booking availability, and public profile URLs) immediately before publication.

## Intake flow

1. Assign a record ID and mark every field with its initial status.
2. Receive the member/owner submission and separate public data from private notes.
3. Confirm names, links, claims, dates, rights, and consent with the relevant owner or rights holder.
4. Mark a record `ready` only when all public fields and associated media are verified.
5. Keep a concise verification record (who confirmed, when, and what scope) outside the public page data.

## Next implementation issue proposal

**35 — Replace placeholder content with verified CyberDJs data**

Scope: replace only the homepage’s confirmed placeholder records using `ready` intake data; preserve empty states where data remains unverified. Include focused validation for links, media alt text, consent/rights metadata, and the existing no-autoplay and booking behavior.
