---
name: refactoring-ui
description: Practical UI/UX visual design rules (based on the book "Refactoring UI" by Adam Wathan & Steve Schoger) for making interfaces look professionally designed — hierarchy, spacing, typography, color palettes, shadows/depth, images, and finishing touches. Use this skill whenever you build, style, restyle, polish, or review any user interface — web pages, app screens, components, dashboards, forms, landing pages, cards, tables, modals, empty states, Tailwind/CSS styling — even if the user only says "make it look better", "this looks off/amateur/cluttered", "clean up the UI", "design review", or asks for a UI without mentioning design at all.
---

# Refactoring UI

Tactical design rules for developers who want interfaces that look *designed* without relying on innate talent. The core insight: most "good looking" UI comes from a handful of learnable decisions — clear hierarchy, generous and systematic spacing, restrained type and color systems, and a few deliberate finishing touches — not from decoration.

## Two modes

**Building new UI** — follow the workflow below, apply the core rules as you write markup/CSS, and pull a starting system from `references/design-tokens.md` if the project doesn't already have one (if it does — Tailwind config, CSS variables, a design system — use *that* instead; consistency with the existing system beats these defaults).

**Reviewing / polishing existing UI** — read the code (and screenshot it if you can render it), then walk `references/review-checklist.md`. Report the highest-impact problems first (hierarchy and spacing usually matter more than shadows), each with a concrete fix. Then apply fixes if asked.

For the full rationale and every technique, read `references/principles.md` — consult the relevant section whenever you're making a decision in that area (e.g. building a color palette → "Color"; hero image with text → "Images").

## Workflow for new UI

1. **Start with a feature, not the shell.** Design the actual functionality (the search form, the list, the card) before nav bars, sidebars, and layout chrome. You don't know what the shell needs until features exist.
2. **Hierarchy first, in grayscale.** Get it working with spacing, size, weight, and contrast before adding color. If it reads well in grey, color only improves it.
3. **Pick a personality deliberately** — font (serif = elegant, rounded sans = playful, neutral sans = safe), primary color, border radius (none = formal, small = neutral, large = playful; never mix), and copy tone. Keep them consistent.
4. **Use systems, not arbitrary values.** Every size, space, font size, weight, color, shadow, and radius comes from a predefined scale. This is what makes UI look consistent and makes decisions fast.
5. **Design the smallest useful version.** Don't imply features that aren't built; nice-to-haves come later. Handle real edge cases (empty states, long content, 0 vs 2000 items).
6. **Finish** with low-effort polish: accent borders, supercharged defaults (icon bullets, custom checkboxes), decorated backgrounds, fewer borders.

## Core rules (the ones that matter most)

**Hierarchy**
- Not everything is equal. Decide what's primary, secondary, tertiary, and make it look that way.
- Don't lean on font size alone — use **weight** and **color** too. Roughly: dark text for primary, mid-grey for secondary, light grey for tertiary; two weights (400/500 normal, 600/700 emphasis); avoid weights under 400 in UI text.
- **Emphasize by de-emphasizing**: if something won't stand out, soften its competitors instead of shouting louder.
- **Labels are a last resort**: format often explains data (`$19.99`, an email); merge label into value ("12 left in stock", "3 bedrooms"); when labels are needed, make them quieter than the data.
- Visual hierarchy ≠ document hierarchy: an `<h1>` section title can be small; style for importance, pick tags for semantics.
- Heavy things (solid icons, bold text) get softer color; light things (thin borders) get more weight instead of harsher color.
- Actions follow a pyramid: one **primary** (solid, high contrast), a few **secondary** (outline/soft background), **tertiary** as links. A destructive action is only big-and-red when it *is* the primary action (e.g. in the confirmation dialog).
- On colored backgrounds, don't use grey or white-with-opacity for secondary text — hand-pick a color with the background's hue, adjusted in saturation/lightness.

**Layout & spacing**
- Start with **too much** white space, then remove. Dense UIs are fine only as a deliberate choice (dashboards).
- Use a **non-linear spacing scale** where adjacent values differ by ≥ ~25% (e.g. 4, 8, 12, 16, 24, 32, 48, 64, 96, 128…).
- Don't fill the screen: give elements the width they need (`max-width`), center or use columns for balance. Try mobile-first at ~400px.
- Grids are a tool, not a religion: fixed-width sidebars + flexible content; `max-width` instead of percentage columns for things with an ideal size.
- Scale components non-proportionally: large headings shrink faster than body text on small screens; large buttons get disproportionately more padding.
- **More space around a group than within it** — label-to-input gap < gap between form groups; space above a heading > space below it.

**Typography**
- Hand-crafted type scale in `px`/`rem` (e.g. 12, 14, 16, 18, 20, 24, 30, 36, 48, 60, 72). No `em` for font sizes (nested compounding breaks the scale).
- Good fonts: neutral sans or the system stack for UI; prefer families with 5+ weights; avoid condensed/short-x-height faces for body text.
- Paragraphs 45–75 characters wide (`max-width: 20–35em`), even if the container is wider.
- Line-height scales inversely with font size and directly with line length: ~1.5–2 for small/wide body text, ~1–1.25 for big headings.
- Align mixed font sizes on a line by **baseline**, not center.
- Left-align text; center only short blocks (≤ 2–3 lines); right-align numbers in tables; hyphenate justified text.
- Tighten letter-spacing on large headlines; widen it on ALL-CAPS text.
- Not every link needs a color — in link-heavy UI use weight/darker color, or hover-only underline for ancillary links.

**Color**
- Think in **HSL** (hue, saturation, lightness), not hex.
- You need a real palette: **8–10 greys**, **1–2 primary colors** and several **accent/semantic colors** (red, yellow, green, maybe more), each with **5–10 shades** (100–900) defined up front. No on-the-fly `lighten()`/`darken()`.
- Build a scale: base (500 ≈ a good button background) → darkest (900, for text) → lightest (100, for tinted backgrounds) → fill in 700/300 → 800/600/400/200. Trust your eyes over math.
- Increase saturation as shades move away from 50% lightness so they don't look washed out. Rotate hue (≤ 20–30°) toward yellow/cyan/magenta to brighten or red/green/blue to darken while keeping color vivid.
- Greys can be tinted: cool (blue) or warm (yellow/orange), saturation increased at the extremes.
- Meet WCAG contrast (4.5:1 normal text, 3:1 large). If white-on-color demands too dark a background, **flip it**: dark colored text on a light tinted background.
- Never rely on color alone — pair with icons, text, or lightness contrast.

**Depth**
- Light comes from above: raised elements get a lighter top edge + small, sharp dark shadow below; inset elements (inputs, wells) get a dark inner shadow at top + lighter bottom edge.
- Shadows mean **elevation** — define ~5 shadows (small for buttons, medium for dropdowns, large for modals) and choose by z-position, not taste. Use them in interaction (lift on drag, shrink on press).
- Two-part shadows: a large soft offset one + a tight dark one; the tight one fades as elevation rises.
- Flat designs still have depth: lighter = closer, darker = further; solid unblurred offset shadows.
- Overlap elements across backgrounds to create layers; separate overlapping images with a background-colored "invisible border".

**Images**
- Use good photos (pro or quality stock) — never plan to swap in phone snaps later.
- Text over images needs consistent contrast: overlay, lower image contrast, colorize (desaturate + multiply fill), or a soft glow text-shadow.
- Everything has an intended size: don't scale small icons up (put them in a colored shape instead) or big icons/logos down (redraw simplified favicons); don't shrink full screenshots — crop or simplify them.
- User uploads: fixed aspect-ratio containers with `object-fit: cover`; prevent background bleed with a subtle inner shadow or semi-transparent inner border.

**Finishing touches**
- Supercharge defaults: icon bullets, big colored quote marks, custom link underlines, brand-colored checkboxes/radios.
- Accent borders (top of card, side of alert, active nav, under a heading) add color cheaply.
- Decorate backgrounds: color change, gentle gradient (hues ≤ 30° apart), low-contrast pattern or shape.
- Empty states are first impressions: illustration + prominent CTA; hide filters/tabs that do nothing yet.
- Use fewer borders — separate with box-shadow, different background colors, or extra spacing.
- Think outside the box: dropdowns can have sections/columns/icons, table cells can combine related data with hierarchy, radio buttons can be selectable cards.

## Output expectations

- When writing code, bake the rules in silently — the user wants a good-looking result, not a lecture. Briefly mention the key design decisions only if they're non-obvious (e.g. "flipped the alert to dark-on-light for contrast").
- When reviewing, be concrete: point at the element, name the rule, give the exact change (`color: hsl(...)`, `gap-6` → `gap-8`, remove the border, etc.). Prioritize by visual impact.
- Respect existing design systems and brand constraints; these rules guide choices within them rather than override them.
