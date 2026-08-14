# Issue #3 — CyberDJs Design System

Scope: concise planning document for GitHub Issue #3.

This document is based only on:

- `AGENTS.md`
- `README.md`
- `.github/agent-pack/MASTER_PROMPT.md`
- `.github/agent-pack/CREATIVE_BRIEF.md`
- `.github/agent-pack/CONTENT_MODEL.md`
- `.github/agent-pack/ISSUE_01_AUDIT.md`
- `.github/agent-pack/ISSUE_02_IA_CONTENT_MODEL.md`
- `index.html`

No production code, CSS, HTML, deployment workflow, build, full repository scan, or live production verification was performed.

## 1. Brand and design principles

CyberDJs should read first as an artist crew, then as a booking destination, then as a CyberCore-connected music technology platform.

Design principles:

- Underground signal: use pirate-radio, frequency, waveform, transmission, and booth-control references.
- Controlled intensity: dark base, strong type, restrained neon, and deliberate contrast instead of full-page glow.
- Human before machine: technology should amplify artists, not replace the crew identity.
- Brutalist rhythm: allow hard grid breaks, sharp section transitions, cropped signal marks, and asymmetric layouts.
- Booking clarity: every high-impact view should keep a visible path to booking.
- No fake cyberpunk: avoid Matrix code, fake terminals, stock DJ imagery, meaningless glitch, startup gradients, and crypto cues.
- Mobile first: layouts should feel designed for small screens, not merely compressed from desktop.

## 2. Color tokens

Recommended semantic tokens:

```css
:root {
  --color-void: #050506;
  --color-panel: #101014;
  --color-panel-raised: #17171d;
  --color-line: #2a2a33;
  --color-text: #f2f0e8;
  --color-text-muted: #a6a398;
  --color-acid: #d7ff2f;
  --color-cyan: #37f0ff;
  --color-magenta: #ff3d9a;
  --color-redline: #ff4b3e;
  --color-warm-metal: #b8ad94;
  --color-focus: #ffffff;
}
```

Usage rules:

- Use `--color-void` as the dominant background.
- Use `--color-panel` and `--color-panel-raised` for navigation, cards, embeds, and form surfaces.
- Use `--color-acid` as the primary action color, especially booking.
- Use `--color-cyan` for signal, waveform, metadata, and interactive accents.
- Use `--color-magenta` sparingly for active states or memorable identity moments.
- Use `--color-redline` only for warnings, destructive states, or high-tension decorative marks.
- Keep text contrast high; never place muted text on low-contrast panel backgrounds without checking WCAG contrast.

## 3. Typography direction

Recommended direction:

- Display: condensed, high-impact sans for CyberDJs identity, section openers, and brutalist statements.
- Body: readable modern sans with generous line height for bios, event copy, booking text, and metadata.
- Mono: limited use for signal IDs, timestamps, event metadata, content tags, and lab/project details.

Type rules:

- Keep copy short, sharp, and specific.
- Avoid oversized hero typography inside cards or compact panels.
- Do not use negative letter spacing.
- Use uppercase sparingly for labels, not body copy.
- Preserve hierarchy: hero identity, section title, card title, metadata, body, legal/helper text.

Suggested scale:

- `display-xl`: hero identity
- `display-lg`: major section statements
- `heading-md`: card and route headings
- `body`: default readable copy
- `body-sm`: metadata and summaries
- `label`: navigation, tags, status pills
- `mono-xs`: timestamps, signal labels, technical project details

## 4. Spacing and grid rules

Spacing tokens:

```css
--space-1: 0.25rem;
--space-2: 0.5rem;
--space-3: 0.75rem;
--space-4: 1rem;
--space-6: 1.5rem;
--space-8: 2rem;
--space-12: 3rem;
--space-16: 4rem;
--space-24: 6rem;
```

Grid rules:

- Use a mobile-first single-column flow.
- Move to two-column editorial layouts where content has meaningful contrast, such as crew plus booking or manifesto plus projects.
- Use a 12-column desktop grid only when it improves alignment; do not make the page feel like a generic landing template.
- Keep content max widths intentional: narrow for copy, wider for artist/music/event grids.
- Use full-width bands for major sections, not nested page cards.
- Cards may be used for repeated items such as artists, events, projects, and media embeds.
- Keep card radius tight, 8px or less.

Breakpoints:

- `sm`: 480px
- `md`: 768px
- `lg`: 1024px
- `xl`: 1280px

## 5. Component inventory

Core layout:

- `Navigation`: simple links, visible booking action, keyboard-friendly mobile menu.
- `Footer`: booking contact, social links, legal/meta links, production identity.
- `SectionHeader`: title, short line, optional signal label.
- `PageShell`: shared layout constraints if a framework is introduced later.

Homepage and route components:

- `HeroSignal`: CyberDJs identity, positioning line, booking CTA, signal/waveform visual.
- `BookingCTA`: repeated booking block with email or form path.
- `ArtistCard`: name, role, genres, location, image/identity mark, links.
- `MusicCard` or `MediaEmbed`: mix/release/video metadata with no autoplay.
- `EventCard`: date, city, venue, status, artist links, ticket/event URL.
- `ProjectCard`: CyberCore/dumpAmp/lab project status, tags, links.
- `ManifestoBlock`: short fragments, not long marketing copy.
- `StatusPill`: active, prototype, upcoming, past, owner-verification states.
- `WaveformVisual`: decorative or data-inspired signal motif that remains accessible.
- `GlitchText`: limited identity treatment only; must degrade cleanly.

Form components for later booking work:

- `TextField`
- `Textarea`
- `SelectField`
- `DateField`
- `SubmitButton`
- `FormStatus`
- `SpamTrap` or equivalent hidden protection pattern

## 6. Motion rules

Motion should feel rhythmic and signal-based, not decorative for its own sake.

Allowed patterns:

- Subtle waveform drift.
- Signal scan or pulse on the hero visual.
- Small hover shifts on cards and booking actions.
- Route/section reveal that does not block reading.
- Active navigation or status changes with short transitions.

Rules:

- Respect `prefers-reduced-motion`.
- Never autoplay audio.
- Avoid constant aggressive flicker, jitter, or glitch.
- Keep motion durations short: roughly 120ms to 300ms for UI, up to 800ms for ambient signal loops.
- Ensure the interface is fully usable with animations disabled.

## 7. Accessibility rules

Minimum requirements:

- Semantic landmarks: `header`, `nav`, `main`, `section`, `footer`.
- One clear `h1` per page.
- Keyboard-visible focus states using a high-contrast focus token.
- Links and buttons must have accessible names.
- Forms must use labels, validation messages, and error summaries where needed.
- Images need meaningful alt text or empty alt text when decorative.
- Color must not be the only indicator for status.
- Embeds must be labeled and must not autoplay.
- Respect reduced motion.
- Maintain readable line length and font size on mobile.
- Test contrast for text, focus, buttons, tags, and status pills before implementation is considered done.

## 8. Implementation recommendations

Given the currently observed static `index.html`, implement the design system incrementally:

1. Start with CSS custom properties for colors, spacing, typography, radius, shadows, focus, and motion.
2. Keep the first implementation static unless a later issue explicitly chooses a framework.
3. Put reusable patterns into plain HTML/CSS classes first; introduce components only when the stack supports them.
4. Keep content data-driven where practical by aligning UI patterns with the Issue #2 models for artists, music, events, projects, and booking.
5. Treat booking as a primary action in navigation, hero, and end-of-page CTA.
6. Keep media embeds lazy or link-based until privacy, performance, and content availability are verified.
7. Use owner-verification flags or comments for provisional artist, event, project, booking, and SEO facts.
8. Avoid third-party scripts unless there is a clear product reason.
9. Do not change deployment workflow while implementing visual tokens.

## 9. Risks

- The current production page is only a minimal deploy placeholder, so the design system has not been tested against real content volume.
- No package manager, framework, asset pipeline, or lint/build command was confirmed in this scoped Issue #3 pass.
- Color and type tokens are recommendations; they still need browser contrast testing during implementation.
- Real artist imagery, social links, music embeds, event data, and booking destination still need owner verification.
- Overusing glitch, neon, or motion could weaken the high-end underground tone and accessibility.
- Future framework adoption could require translating these tokens into a component-specific format.

## 10. Can Issue #3 be closed?

Yes, if Issue #3 is limited to creating a concise design-system planning document.

No, if Issue #3 requires CSS/HTML implementation, production visual redesign, component extraction, asset creation, build/test execution, accessibility testing, or live production verification. Those activities belong to later implementation issues.
