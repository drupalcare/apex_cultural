# APEX Cultural

Cultural-institution sub-theme for [APEX](https://www.drupal.org/project/apex). Cinematic-hero homepage with three landing layouts (event / exhibition / performance, person / artist / curator, location detail). Targets museums, art galleries, theaters, opera houses, performing arts venues.

## Overview

apex_cultural is the catalog's gallery-neutral sub-theme. Per the [APEX Sub-Theme Catalog](../../docs/planning/APEX-SUBTHEME-CATALOG.md):

- **Audience**: museums, art galleries, theaters, opera houses, cultural institutions, performing arts venues
- **Visual identity**: Cormorant Garamond classical serif (display) + Inter readable sans (body), Stone 900 warm-charcoal primary + Amber 800 institutional-brass accent
- **Homepage archetype**: Cinematic hero
- **Landing layouts**: event (exhibition / performance), person (artist / curator), location detail
- **Content emphasis**: event (exhibitions, performances, lectures), person (artists, curators, performers), location (galleries, theaters), case_study (exhibition deep-dives), resource (digital collections, education materials)

## Audience

Sites where the work is the content and the chrome is silent. Drupal already powers Getty, Walker Art Center, Smithsonian, Tate, MoMA, the Met. Per AAM TrendsWatch + MCN reports, digital expansion + virtual experiences + membership prominence are the 10-year direction; per ADA + WCAG accessibility mandates + public-trust mission, AAA-leaning accessibility is essential. apex_cultural makes virtual-tour + membership + accessible-tombstone-format first-class concerns.

## Visual identity

| Aspect | Choice |
|---|---|
| Display font | Cormorant Garamond (EB Garamond / Garamond / Book Antiqua / Palatino / Georgia / Times fallback) — classical serif with signage-influenced silhouette; gallery-wall feel without editorial-magazine weight |
| Body font | Inter (system fallback) — readable sans for didactic copy + chrome |
| Type scale | H1 clamp(2.25rem, 4vw + 1rem, 4rem); body 16px / 1.6 line-height; hero clamp(2.5rem, 5vw + 1rem, 5rem) |
| Palette | Stone 900 `#1c1917` warm charcoal primary + Stone 500 `#78716c` gallery secondary + Amber 800 `#92400e` institutional brass accent (overridable via `apex_schemes` for institution brand standards) |
| Density | Generous; image-led; let work breathe |
| Reading measure | 62ch (didactic / program-notes density) |
| Layout direction | LTR + RTL via logical properties |
| Accessibility | WCAG 2.2 AA baseline, AAA where possible per public-trust mission. 3px brass focus ring. 44px+ touch targets for older-visitor accessibility. |

## Layouts

### Homepage — Cinematic hero

Region map per the catalog:

```
[apex_top_bar — visit / tickets / become-a-member]
[apex_header — logo + utility nav]
[apex_main_navigation — visit / exhibitions / collections / events / education / about]
[apex_hero — apex-cultural-exhibition-hero (full-bleed featured exhibition)]
[apex_content_pre — current exhibitions strip (apex-cultural-event-listing or hero cards)]
[apex_content — upcoming events + education + apex-cultural-artwork-card grid (collection highlights)]
[apex_content_post — apex-cultural-membership-cta + visit info + hours]
[apex_footer — visit + accessibility + membership + plan-an-event + careers]
```

### Landing layouts

| Archetype | Drupal template | Content type |
|---|---|---|
| Event (exhibition / performance) | `node--apex-event--full.html.twig` | apex_event |
| Person (artist / curator) | `node--apex-person--full.html.twig` | apex_person |
| Location detail | `node--apex-location--full.html.twig` | apex_location |

## SDC components

Per the catalog spec — 5 components ship with apex_cultural:

- `apex-cultural-exhibition-hero` — cinematic full-bleed exhibition image with overlay content card (curator + dates + venue + Tickets CTA); cinematic side-by-side at wide viewports, stacked at narrow
- `apex-cultural-artwork-card` — collection / artwork tombstone (artist + italicized title + year + medium + dimensions + accession number + on-view indicator); image preserves natural aspect ratio (no forced crop)
- `apex-cultural-event-listing` — performance / lecture listing with three-column date-block / content / CTA layout at wide viewports; supports free / sold-out states
- `apex-cultural-membership-cta` — membership tier card (charcoal canvas with brass accents); 1-3 tiers with optional "recommended" highlight; final Become-a-member CTA + member-count social proof
- `apex-cultural-virtual-tour` — AR / VR / 360° / video embed slot; poster + play-overlay + technology badge; reduced-motion-compliant transitions

Components live in `components/<name>/` per the [sub-theme contract](../../docs/architecture/sub-theme-contract.md#sdc-components-contract).

## Demo content

apex_cultural's demo content pack (`content/`) imports ~50 nodes via `drush apex:import-demo apex_cultural`:

| Content type | Count |
|---|---|
| apex_event (exhibitions + performances) | 12 |
| apex_person (artists + curators) | 12 |
| apex_location (galleries + theaters) | 4 |
| apex_resource (collection items) | 10 |
| apex_case_study (exhibition deep-dives) | 6 |
| apex_resource (education materials) | 6 |

## Installation

```bash
composer require drupal/apex_cultural
drush theme:enable apex_cultural
drush config:set system.theme default apex_cultural
drush cr
```

The sub-theme **automatically enables every APEX module** the parent theme depends on.

To install the demo content pack:

```bash
drush apex:import-demo apex_cultural   # Drush command shipped by W5 Phase A scaffolding
```

## Customization

Per the [APEX cascade-layer contract](../../docs/architecture/css-cascade-layers.md):

- **Plain CSS** in this sub-theme beats every `@layer apex.*` rule. Brand assertions (Cormorant Garamond + Inter pair, gallery-neutral palette, no-border-radius CTA discipline) go here.
- **Layered CSS** (`@layer apex.base`, `@layer apex.components`, etc.) opts into a default that admin Live Editor / modules can override.

Cultural institutions typically swap charcoal primary, brass accent, and gallery-secondary via apex_schemes for their brand standards. The engine derives the full per-region palette from those primary/secondary/accent anchors.

## Accessibility / public-trust mission

- **AAA-leaning baseline.** ADA + WCAG mandates are minimums; cultural institutions are public-trust entities and should target AAA where possible. apex_cultural's 3px focus ring, 44px+ touch targets, generous line-heights, and required `image_alt` props on every image-led component support that target.
- **Artwork descriptions are accessibility content.** The `apex-cultural-artwork-card` SDC requires `image_alt` (not just `image_src`); per AAM digital-accessibility guidance, accessible artwork descriptions are part of the institution's mission, not an a11y afterthought.
- **Virtual-tour fallbacks.** The `apex-cultural-virtual-tour` SDC ships with explicit `requires_headset` prop so headset-required VR experiences disclose that requirement up-front; non-VR fallbacks (360° photos, video) are first-class technology options.

## Dependencies

- Drupal core `^11.1`
- `apex_theme` (parent theme — auto-pulls every APEX module the parent depends on)

## Screenshots

_Pending Phase 5 docs polish per [W2 v1-readiness](../../docs/planning/workstreams/2-apex-v1-readiness.md)._

## Changelog

See [CHANGELOG.md](./CHANGELOG.md).

## Troubleshooting

_Pending Phase 5 docs polish. For now, see [APEX-KNOWLEDGE-BASE.md](../../docs/APEX-KNOWLEDGE-BASE.md) and the [APEX briefing](../../docs/APEX-BRIEFING.md)._

## License

GPL-2.0-or-later. Part of the [APEX](https://www.drupal.org/project/apex) design system. Sub-themes are FREE per the [APEX commercial structure](../../docs/planning/workstreams/INDEX.md#commercial-structure-locked-expanded-2026-04-26).
