# Refactoring UI — Full Principles

Paraphrased and made actionable from *Refactoring UI* (Wathan & Schoger). Each rule has the why and how to apply it in code.

## Contents
1. Starting from scratch
2. Hierarchy
3. Layout & spacing
4. Typography
5. Color
6. Depth
7. Images
8. Finishing touches
9. Leveling up

---

## 1. Starting from scratch

**Start with a feature, not a layout.** An app is a set of features. Before a few of them exist, you can't know what the navigation or shell needs. So build the actual thing first. For a flight search, that means the origin, destination and date fields plus the search button. Sometimes the shell turns out to be unnecessary.

**Detail comes later.** Early on, skip decisions about typefaces, shadows and icons. Sketch or rough out layouts quickly. Work in **grayscale** first. Without color, spacing, contrast and size have to create the hierarchy, and a UI with strong hierarchy is easy to enhance with color later. Mockups are disposable, so don't over-invest in them.

**Don't design too much.** Work in short cycles: design a simple version of one feature, build it, and fix the problems you find in the real thing. Then move to the next feature. Edge cases are easier to solve in a working UI than in your imagination.

**Be a pessimist.** Don't design features you aren't ready to build. For example, if the comment UI includes attachments that turn out to be hard, the whole comments feature gets stuck. Design the smallest useful version so there's always something shippable. Nice-to-haves come later.

**Choose a personality.** A few concrete levers set it:
- *Font*: serif for elegant or classic, rounded sans for playful, neutral sans for plain (lets other elements carry the personality).
- *Color*: blue is safe and familiar, gold reads expensive, pink reads fun. Mostly trust how a color feels.
- *Border radius*: none feels formal or serious, small is neutral, large is playful. Be consistent, because mixing square and rounded corners looks worse than either.
- *Language*: formal copy feels professional, casual copy feels friendly. Words are everywhere in a UI.
- If you're unsure, look at other sites your audience uses. Don't copy direct competitors.

**Limit your choices.** Unlimited options cause paralysis: 12px vs 13px, 10% vs 15% shadow opacity. Define systems in advance, such as 8–10 shades per color and a fixed type scale. Then **design by elimination**: guess the middle value, try its neighbors on the scale, and keep whichever looks best. Systematize font size, weight, line-height, color, margin, padding, width, height, shadows, radius, border width and opacity. Never make the same micro-decision twice.

---

## 2. Hierarchy

**Not all elements are equal.** Visual hierarchy is how important elements look relative to each other. It's the single biggest factor in whether a UI looks designed. When everything competes, the UI feels noisy. Deliberately de-emphasize secondary and tertiary content and highlight what matters. That alone transforms a UI without changing its colors or fonts.

**Size isn't everything.** If you rely only on font size, primary text ends up too big and secondary text too small. Use **weight** and **color** as well:
- Colors: dark for primary (headline), grey for secondary (date), lighter grey for tertiary (footer fine print).
- Weights: normal (400/500) for most text, bold (600/700) for emphasis. Avoid weights below 400 at UI sizes. To de-emphasize, use a lighter color or a smaller size instead.

**Don't use grey text on colored backgrounds.** Grey works on white because it lowers contrast, and lower contrast is what creates the hierarchy. On a colored background, grey looks muddy, and white at reduced opacity looks washed out or disabled (and on images the background shows through it). Instead, hand-pick a color with the **same hue** as the background and adjust saturation and lightness until it reads as secondary.

```css
/* on a hsl(220 70% 45%) panel */
.panel .muted { color: hsl(220 80% 85%); }  /* not rgba(255,255,255,.6), not grey */
```

**Emphasize by de-emphasizing.** If the active nav item won't pop, soften the inactive items. If a sidebar competes with the main content, remove the sidebar's background so it sits on the page.

**Labels are a last resort.** A `Label: value` layout gives every field equal weight.
- Often you need no label because the format tells you: an email, a phone number, a price, a department shown under a name.
- Combine the label and value: "12 left in stock", "3 bedrooms".
- When you need a label (for scannable, similar data like dashboard stats), make it secondary: smaller, lower contrast, lighter weight.
- Exception: on spec-sheet style pages where users scan *for* the label ("Depth"), emphasize the label, but only slightly (a darker label, a slightly lighter value).

**Separate visual hierarchy from document hierarchy.** Choose `h1`–`h6` for semantics, not size. In app UIs, section titles often act like labels and should be small, because the content is the focus. Sometimes they can be visually hidden but kept for accessibility.

**Balance weight and contrast.** Bold feels emphasized because it covers more pixels. Solid icons are heavy, so next to text they dominate. Balance them with a **softer color**. The reverse also works: a thin 1px border that's too faint shouldn't be darkened (that looks harsh). Make it **thicker** (2px) at the soft color.

**Semantics are secondary (for actions).** Each page has a pyramid of actions:
- **Primary** (usually one): obvious, with a solid high-contrast background.
- **Secondary**: clear but not prominent, using an outline or a low-contrast background.
- **Tertiary**: discoverable but unobtrusive, styled like a link.
- **Destructive** ≠ automatically big and red. If deleting isn't the page's main action, give it secondary or tertiary styling. Use big red styling in the confirmation step, where it *is* the primary action.

---

## 3. Layout & spacing

**Start with too much white space.** Usually white space gets added until things stop looking bad, which yields "not bad", not "great". Instead, start with far too much and remove it. What looks like a bit too much for one element is often just right in the full UI. Dense layouts (data-heavy dashboards) are valid, but make density a deliberate choice, not the default.

**Establish a spacing and sizing system.** A linear scale like "multiples of 4" doesn't help you choose between 120 and 125. What matters is the **relative** difference: 12→16 is +33%, while 500→520 is only +4%. Keep adjacent values at least ~25% apart. Base the scale on 16px, with tight steps at the small end that widen as values grow. Example: `4 8 12 16 24 32 48 64 96 128 192 256 384 512 640 768`. Workflow: pick a value, and if it's not enough, the next step up is probably right. You get speed and a subtle consistency.

**You don't have to fill the whole screen.** If 600px is enough, use 600px. Not every section needs to be full-width because the nav is. Tips:
- Shrink the canvas and design mobile first (~400px), then adjust whatever felt like a compromise at larger sizes.
- If a narrow element looks unbalanced in a wide layout, **split it into columns** (e.g. a form with a separate column of supporting text) rather than widening it.
- Conversely, don't cram things if you need the space.

**Grids are overrated.** A 12-column grid is just fluid percentages, and not everything should be fluid.
- Sidebars get a **fixed width** sized to their content. The main area flexes (and can use its own internal grid). A percentage sidebar grows uselessly wide on big screens and gets cramped on small ones.
- Components with an ideal size (a login card, a modal) get a `max-width` and shrink only when the viewport is smaller. Percentage-column tricks can make a card *wider* on medium screens than on large ones, which makes no sense.
- Don't use percentages unless you actually want the element to scale.

**Relative sizing doesn't scale.** A headline at `2.5em` of 18px body text works on desktop. On mobile, with 14px body, it becomes 35px, far too big (20–24px is right). Big elements must shrink **faster** than small ones on small screens, so define sizes independently per breakpoint. Within components, don't tie padding to font size with `em`. Larger buttons should get disproportionately more padding and smaller buttons tighter padding, so they feel genuinely larger or smaller rather than zoomed.

**Avoid ambiguous spacing.** When there's no border or background to group things, spacing does the grouping. **Space between groups must exceed space within them.**
- Forms: label→input gap < the gap between one form group and the next.
- Articles: more space above a heading than below it, so it attaches to its section.
- Lists: the gap between bullets should be larger than the line gap within a wrapped bullet.
- The same applies horizontally (e.g. inline groups of icon+text).

---

## 4. Typography

**Establish a type scale.** Most UIs have every size from 10 to 24px. Linear scales fail here too. Modular scales (ratios like 4:5, 2:3, golden) produce fractional pixels (31.25, 39.06) that browsers round inconsistently, and their steps are too coarse for UI work. **Hand-pick** the scale instead, e.g. `12 14 16 18 20 24 30 36 48 60 72` (px). Define it in `px` or `rem`, **never `em`**: nested `em` sizes compound (e.g. 0.875em inside 1.25em = 17.5px), which is off-scale.

**Use good fonts.**
- The safe choice is a neutral sans (Helvetica-like), or the system stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Noto Sans", Ubuntu, Cantarell, "Helvetica Neue", sans-serif`.
- Prefer families with **5+ weights** (on Google Fonts, filter for 10+ styles to include italics). It's a rough proxy for craftsmanship.
- Optimize for legibility. Headline fonts have tight spacing and short x-heights. Don't use condensed or short-x-height faces for body UI text.
- Popular fonts are popular for a reason. Sort by popularity, especially when picking a serif with personality.
- Inspect sites you admire and borrow their choices.

**Keep line length in check.** Aim for 45–75 characters per line: `max-width: 20em`–`35em` on paragraphs. Keep paragraphs narrow even when images or other elements in the same content area are wider. Mixed widths look more polished.

**Baseline, not center.** When different font sizes share a line (a big card title with small actions on the right), align them by **baseline** (`align-items: baseline`), not vertical center.

**Line-height is proportional.**
- It scales with line **length**: narrow text can use ~1.5, wide text may need up to 2, because the eye has further to travel back to the next line.
- It scales **inversely** with font size: small text needs more, and big headings can use ~1–1.25.

**Not every link needs a color.** Links inside paragraphs must stand out. In UIs where nearly everything is a link, that treatment is overbearing, so use heavier weight or a darker color instead. For ancillary links, show an underline or color only on hover.

**Align with readability in mind.**
- Left-align most text (in left-to-right languages).
- Center only headlines and short independent blocks (≤ 2–3 lines). If one centered block is too long, shorten the copy.
- Right-align numbers in tables so decimals line up (and use `font-variant-numeric: tabular-nums`).
- If you justify text, also set `hyphens: auto`. Justify only for print-like, formal looks.

**Use letter-spacing effectively.** Trust the typeface designer by default, with two exceptions:
- **Tighten large headlines** set in a UI font with wide default spacing (e.g. `letter-spacing: -0.02em`). Don't do the reverse, since headline fonts rarely work small.
- **Widen ALL-CAPS text** (e.g. `letter-spacing: 0.05em`), because uppercase letters lack the ascenders and descenders that make words distinct.

---

## 5. Color

**Ditch hex for HSL.** Hex and RGB hide relationships between colors. HSL maps to perception:
- **Hue** is the angle on the color wheel (0 red, 120 green, 240 blue).
- **Saturation** is vividness (0% = grey, and then hue is irrelevant).
- **Lightness** runs from 0% black to 100% white, with 50% the pure hue.
- HSL ≠ HSB. In HSB, 100% brightness is white only at 0% saturation. Browsers speak HSL.

**You need more colors than you think.** Five-color "palette generator" results can't build a UI. You need:
- **Greys**: 8–10 shades, because almost everything (text, backgrounds, panels, form controls) is grey. Start with a very dark grey rather than pure black, which looks unnatural.
- **Primary**: 1–2 brand colors, each with 5–10 shades. Ultra-light shades serve as tinted backgrounds, dark shades as text.
- **Accents**: attention colors (yellow, pink, teal for "new") and semantic ones (red = danger, yellow = warning, green = success), each with shades. Add more for categorization (charts, calendars, tags). A complex UI can need ~10 colors × 5–10 shades.

**Define your shades up front.** Don't generate them on the fly with `lighten()`/`darken()`, or you'll end up with 35 nearly identical blues.
1. **Base (500)**: the shade that works as a button background. Choose it by eye; there's no magic lightness value.
2. **Edges**: **900** is the darkest, used for text. **100** is the lightest, used for tinted backgrounds. An alert component is a good test bench for both.
3. **Fill gaps**: 700 and 300 first (perfect midpoints), then 800, 600, 400, 200.
4. Greys: same process. The darkest is your darkest text; the lightest is a subtle off-white background.
5. Tweak by eye once you use them in real designs. Avoid adding new shades later, or the system collapses.

**Don't let lightness kill your saturation.** Saturation looks weaker near 0% and 100% lightness, so **raise saturation** for very light and very dark shades to keep them from looking washed out.
- **Perceived brightness** varies by hue. Yellow, cyan and magenta (60°, 180°, 300°) look bright; red, green and blue (0°, 120°, 240°) look dark.
- To lighten a color without losing intensity, **rotate hue toward the nearest bright hue**. To darken it, rotate toward the nearest dark hue. Example: yellow shades rotate toward orange as they darken, so they look warm and rich instead of brown.
- Keep rotation within 20–30°, or it becomes a different color. Combine it with lightness changes.

**Greys don't have to be grey.** Tint greys with a little saturation. Blue-tinted greys feel cool; yellow or orange-tinted greys feel warm. Increase the saturation at the light and dark ends to keep the temperature consistent. How much tint you use is up to you.

**Accessible doesn't have to mean ugly.** WCAG: ≥ 4.5:1 contrast for normal text (under ~18px), ≥ 3:1 for large text.
- White text on color often needs a very dark background, and that grabs too much attention. **Flip the contrast**: use dark colored text (e.g. 800/900) on a light tinted background (100).
- For colored secondary text on a dark colored panel, adjusting only lightness pushes it toward white. **Rotate the hue toward a brighter hue** (cyan, magenta, yellow) to gain contrast while staying colorful.

**Don't rely on color alone.** Colorblind users can't separate red and green trends, so add icons (↑/↓) or text. In charts, vary **lightness/contrast** between series rather than relying only on distinct hues. Color should reinforce, never be the only signal.

---

## 6. Depth

**Emulate a light source.** Light comes from above. Figure out the profile you want, then mimic the light.
- **Raised** (e.g. a button): show a slightly **lighter top edge** (top border or `inset 0 1px 0` with a hand-picked lighter color, not white overlay, which kills saturation). Add a **small, dark, sharp shadow below** (`0 1px 3px`, a couple of px of blur, positive y-offset).
- **Inset** (a well, input or checkbox): a **lighter bottom edge** (bottom border or `inset 0 -1px 0`) plus a **dark inset shadow at the top** (`inset 0 2px 2px`).
- Don't chase photorealism. A few cues are enough; too many make the UI busy.

**Use shadows to convey elevation.** Shadows place elements on a z-axis, and closer elements draw more focus.
- Small, tight shadows: slightly raised (buttons).
- Medium: dropdowns and popovers.
- Large, blurry: modals.
- Define about **5 shadows**, smallest and largest first, then fill the middle roughly linearly.
- Use them in interaction: add a bigger shadow when an item is picked up for dragging, and shrink or remove the shadow when a button is pressed. Choose shadows by **where the element sits**, not by how the shadow looks.

**Shadows can have two parts.**
1. A large, soft shadow with a big y-offset and big blur: the direct light shadow.
2. A tight, darker shadow with a small offset and small blur: the ambient occlusion right under the object.
As elevation rises, the tight shadow fades. Make it distinct at the lowest level and nearly invisible at the highest.

**Even flat designs have depth.**
- Color: lighter feels closer, darker feels further away. An element lighter than the background feels raised; darker feels inset.
- Solid shadows: a short vertical offset with **zero blur** (`0 4px 0 hsl(...)`) keeps the flat aesthetic.

**Overlap elements to create layers.** Offset a card across the boundary of two background sections, make an element taller than its parent, or let carousel controls overhang the edges. When overlapping images, give them an "invisible border" in the background color (e.g. `box-shadow: 0 0 0 4px var(--bg)`) so they don't clash.

---

## 7. Images

**Use good photos.** Bad photos ruin good designs. Hire a professional for specific needs, or use quality stock (e.g. Unsplash) for generic ones. Never design around placeholders expecting to swap in smartphone shots later.

**Text needs consistent contrast.** Photos have light and dark regions, so no single text color works everywhere. Reduce the image's dynamics:
- **Overlay**: a semi-transparent black overlay behind light text, or white behind dark text.
- **Lower the image contrast** (and compensate brightness). This gives more control than an overlay.
- **Colorize**: lower contrast → desaturate → solid fill with `mix-blend-mode: multiply`. It also ties the image to brand colors.
- **Text shadow as glow**: large blur, zero offset, subtle. Combine it with a smaller contrast reduction.

**Everything has an intended size.**
- Don't scale up icons drawn for 16–24px; at 3–4× they look chunky. Instead, place the small icon inside a larger shape with a background color.
- Don't shrink full screenshots (16px text becomes 4px). Screenshot a smaller layout (e.g. tablet), crop a partial screenshot, or draw a simplified UI with lines in place of text.
- Don't scale down large icons or logos, e.g. for favicons. Redraw a simplified version at the target size.

**Beware user-uploaded content.**
- Control shape and size: fixed containers with the image centered and cropped (`object-fit: cover` or `background-size: cover`).
- Prevent background bleed (an image with a white background on a white UI): a subtle **inner shadow** (`box-shadow: inset 0 0 0 1px hsl(0 0% 0% / .1)`) or a semi-transparent inner border. Solid borders clash with the image's colors.

---

## 8. Finishing touches

**Supercharge the defaults** before adding new elements:
- Replace bullets with icons (checkmarks, arrows, or topical ones like a padlock for security features).
- Turn testimonial quote marks into large, colored visual elements.
- Give links custom styling: a weight and color change, or a thick colored underline that partly overlaps the text.
- Use custom checkboxes and radios in brand colors (`accent-color` is the easy route).

**Add color with accent borders.** A colored strip across the top of a card, beside an alert, under the active nav item, as a short bar under a headline, or across the top of the whole page. It needs no graphic design skill.

**Decorate your backgrounds.**
- Change the background color of a panel or page section.
- Use a subtle gradient with two hues **≤ 30° apart**.
- Add a low-contrast repeating pattern (full background or along one edge).
- Place a simple shape, a chunk of pattern, or a simplified illustration (e.g. a world map) in specific spots.
- Keep contrast low so decoration never hurts readability.

**Don't overlook empty states.** For features that depend on user content, the empty state is the first impression. Use an illustration or image plus an emphasized call to action. Hide tabs, filters and other controls that do nothing until content exists.

**Use fewer borders.** Too many borders feel busy. Alternatives:
- A box-shadow outline (works best when the element's color differs from the background).
- Slightly different background colors for adjacent areas (if you have both a color difference and a border, drop the border).
- Extra spacing.

**Think outside the box.** Question default component shapes.
- Dropdowns can have sections, multiple columns, supporting text and colored icons.
- Tables: combine related non-sortable columns into one cell with internal hierarchy (e.g. name bold with email grey beneath), and add avatars, images or colored badges.
- Radio buttons for important choices can become **selectable cards**.

---

## 9. Leveling up

- When you see a design you like, ask what the designer did that **you wouldn't have thought to do**: an inverted datepicker background, a button inside a text input, a two-color headline.
- **Rebuild interfaces you admire** without looking at devtools. The differences you have to chase down teach tricks like tighter heading line-height, tracking on uppercase text and layered shadows.
