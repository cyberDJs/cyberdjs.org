# Issue #32 — Design Polish After Logo Integration

## Scope

Focused visual refinement of the static homepage after the Issue #30 header-logo integration. No content model, metadata, booking behavior, deployment configuration, external asset, font, script, or dependency changes were made.

## Visual changes made

- Refined the header's compact spacing, increased its visual separation, and gave the existing optimized 32px logo a restrained cyan halo for better integration with the site palette.
- Rebalanced the ambient background and hero toward cyan and blue, with a smaller acid accent and reduced magenta emphasis.
- Updated the signal panel and waveform to use the logo-aligned cyan/blue direction; the existing scan and waveform motion are slower and less prominent.
- Tightened CTA borders, highlights, hover feedback, section dividers, and card surfaces for a more coherent visual rhythm.
- Kept the existing dark underground identity, tight radii, and booking prominence intact.

## Files changed

- `index.html`
- `.github/agent-pack/ISSUE_32_DESIGN_POLISH.md`

## Accessibility notes

- The skip link, semantic structure, header link label, empty decorative logo alt text, and visible high-contrast focus treatment are unchanged.
- The logo still declares explicit 32 by 32 pixel dimensions, preventing image-driven layout shift.
- Existing `prefers-reduced-motion` handling continues to disable transitions and animations; the ambient signal animations were only slowed, not expanded.
- Interactive feedback continues to use both color and shape/elevation changes.

## Performance notes

- No new assets, fonts, scripts, embeds, or dependencies were added.
- Effects use existing CSS gradients, borders, and short transitions; no additional animation loops were introduced.
- The header continues to use the existing optimized 128px logo derivative, not a large source asset.

## Remaining risks

- Browser-based desktop and compact-mobile visual review was not run in this scoped pass.
- `backdrop-filter` retains its existing progressive-enhancement behavior and may render without blur in unsupported browsers.
- Final contrast and focus appearance should be checked on deployed hardware/browser combinations before merge.
