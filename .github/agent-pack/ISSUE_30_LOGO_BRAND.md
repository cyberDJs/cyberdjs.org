# Issue #30 — Logo and Brand Assets

## Asset inventory

The supplied large raster masters are retained, without modification, under `assets/brand/source/`:

- `cyberdjs-icon-fullcolor-source.png`
- `cyberdjs-logo-display-fullcolor-source.png`
- `cyberdjs-logo-mono-black-source.png`
- `cyberdjs-logo-mono-white-source.png`
- `cyberdjs-logo-primary-fullcolor-source.png`

Each source/master asset is 1254 by 1254 pixels. They remain the approved inputs for future derivatives and are not used in the header.

Optimized derivatives are available in `assets/brand/`:

- `cyberdjs-icon-header-128.png` — 128 by 128 pixels, header icon
- `cyberdjs-icon-256.png` — 256 by 256 pixels, general icon derivative
- `cyberdjs-logo-primary-512.png` — 512 by 512 pixels, primary-logo derivative

## Usage

`index.html` uses `cyberdjs-icon-header-128.png` in the primary-header brand link. Its fixed 32 by 32 pixel presentation and `object-fit: contain` preserve the supplied square artwork's proportions and keep the mobile header compact.

The 256px icon and 512px primary-logo derivatives are retained for future verified placements. No social-preview metadata was added because no dedicated local social-preview image was created for that purpose.

## Accessibility

The logo image has empty alternative text because the adjacent visible `CyberDJs` text and the link's existing `aria-label="CyberDJs home"` provide the link's accessible name. Explicit image dimensions reserve its layout space, and the existing visible keyboard focus treatment remains unchanged.

## Remaining brand limitations

No SVG logo source was supplied. The header therefore uses the local PNG icon rather than an SVG. The large source/master PNGs are approximately 968 KB to 1.6 MB each and are intentionally kept out of the header; the optimized 128px derivative is approximately 34 KB. A vector source would still be preferable before expanding brand usage.
