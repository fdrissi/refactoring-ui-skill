# UI Review Checklist

Use this to audit an existing screen or component. Work top-down. Earlier sections usually have the biggest visual impact. For each problem, report **element → rule → concrete fix**. Skip items that don't apply.

## 1. Hierarchy (highest impact)
- [ ] Is it obvious within 2 seconds what the most important thing is? If everything looks equally loud, pick a primary element and quiet the rest.
- [ ] Is hierarchy created with weight and color, not just font size? Look for oversized headings and tiny secondary text.
- [ ] Are there at most ~3 text colors (primary, secondary, tertiary) and ~2 weights? Any font weights under 400 on small text?
- [ ] Does the UI use `Label: value` pairs where the format or context would do, or where label and value could merge ("3 bedrooms")? Are the necessary labels quieter than the data?
- [ ] Are section titles sized by importance rather than by their `h1`/`h2` tag?
- [ ] Do solid icons overpower adjacent text? (Soften their color.) Do faint borders look harsh when darkened? (Thicken them instead.)
- [ ] Is there exactly one primary action per view? Are secondary actions outline or soft, and tertiary ones link-style? Is a non-primary destructive action styled big and red when it shouldn't be?
- [ ] Is there grey text or `rgba(255,255,255,.x)` text on a colored background? Replace it with a same-hue color.

## 2. Spacing & layout
- [ ] Does it feel cramped? Try roughly 1.5–2× the padding and gaps, then pull back.
- [ ] Are spacing and size values arbitrary (13px, 18px, 22px, 37px)? Snap them to the scale.
- [ ] Is anything stretched full-width that has a natural width (forms, login cards, paragraphs, modals)? Add `max-width`.
- [ ] Are sidebars percentage-width? Make them a fixed width with flexible content.
- [ ] Is grouping ambiguous? Space between groups must exceed space within them: label↔input vs. between fields, above a heading vs. below it, between list items vs. line-height.
- [ ] On mobile, are headings still desktop-sized (e.g. via `em` ratios)? Big elements should shrink faster.
- [ ] Do different-sized buttons just look zoomed? Adjust their padding non-proportionally.

## 3. Typography
- [ ] Count distinct font sizes. More than ~8–10 means you need a type scale. Are any sizes in `em`?
- [ ] Is the font suitable for UI (neutral, 5+ weights, decent x-height)? Is a condensed or display face used for body text?
- [ ] Is paragraph line length within 45–75 characters?
- [ ] Line-height: body text ~1.5 or more (taller for wide text), large headings ~1–1.25?
- [ ] Are mixed font sizes on one line aligned by baseline?
- [ ] Is text over 2–3 lines centered? Are table numbers right-aligned (tabular numerals)? Is justified text missing hyphenation?
- [ ] Do ALL-CAPS labels need extra letter-spacing? Would large headings benefit from slightly tighter tracking?
- [ ] In a link-dense UI, is every link loudly colored? Tone the ancillary ones down.

## 4. Color
- [ ] Is there a defined palette (greys 8–10 shades, primary, and semantic accents with shades), or ad-hoc hex values and `lighten()`/`darken()` calls?
- [ ] Is pure `#000` used for text? Use a very dark (optionally tinted) grey instead.
- [ ] Do very light or dark shades look washed out? Increase their saturation, or rotate hue slightly.
- [ ] Are greys flat grey when a slight warm or cool tint would suit the personality?
- [ ] Contrast: normal text ≥ 4.5:1, large text ≥ 3:1. Do white-on-color elements force a heavy dark background? Flip them to dark text on a light tint.
- [ ] Is any meaning carried by color alone (red/green deltas, chart series, status dots)? Add an icon, text, or a lightness difference.

## 5. Depth
- [ ] Are shadows random, or do they come from a small elevation scale (≈5 levels) that matches z-position (button < dropdown < modal)?
- [ ] Do raised elements follow light-from-above (lighter top edge, shadow below)? Do inputs and wells read as inset?
- [ ] Would a two-part shadow (soft large + tight dark) look crisper than a single blurry one?
- [ ] Do interactions use elevation (lift on drag, press-in on click)?
- [ ] Could overlapping elements across section boundaries add layering to a flat-looking layout?

## 6. Images
- [ ] Are the photos high quality, or placeholder or amateur?
- [ ] Is text over images consistently readable (overlay, reduced contrast, colorize, or glow shadow)?
- [ ] Are small icons blown up? (Put them in a colored shape.) Are logos or icons shrunk into mush? Are screenshots scaled down until unreadable?
- [ ] Are user uploads in fixed-ratio containers with `object-fit: cover`? Do images bleed into the background? (Use a subtle inset shadow or semi-transparent inner border.)

## 7. Finishing touches & states
- [ ] Too many borders? Replace them with box-shadow, a background-color difference, or more spacing.
- [ ] Is there a designed empty state (illustration + CTA, with useless controls hidden)?
- [ ] Are there cheap wins: icon bullets, accent borders, brand-colored checkboxes and radios, a styled quote, a subtle background color, gradient or pattern?
- [ ] Is a component stuck in its default form when a richer one would serve better (multi-column dropdown, combined table cells with hierarchy, selectable cards instead of radios)?
- [ ] Is the personality consistent: one border-radius family, a coherent font, color and tone of copy?

## Report format

```
## Top issues (fix these first)
1. <element> — <rule>. Fix: <exact change>.
...
## Polish
- ...
## What's already working
- ...
```
