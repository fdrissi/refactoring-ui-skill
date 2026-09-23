# Starter Design Tokens

A starting system that follows the book's rules. Use it only when the project has no existing system. If Tailwind is present, its default scales already follow these principles (spacing, type, shadows, 50–950 color shades), so use Tailwind's classes rather than these variables.

Adjust hues to the chosen personality. Tune shades by eye once they're in real UI.

```css
:root {
  /* Spacing & sizing: non-linear, adjacent steps ≥ ~25% apart (base 16px) */
  --space-1: 4px;   --space-2: 8px;   --space-3: 12px;  --space-4: 16px;
  --space-5: 24px;  --space-6: 32px;  --space-7: 48px;  --space-8: 64px;
  --space-9: 96px;  --space-10: 128px; --space-11: 192px; --space-12: 256px;
  /* widths: 384 512 640 768 … use as max-widths for cards, forms, modals */

  /* Type scale: hand-picked, px/rem only (never em) */
  --text-xs: 0.75rem;  /* 12 */  --text-sm: 0.875rem; /* 14 */
  --text-base: 1rem;   /* 16 */  --text-lg: 1.125rem; /* 18 */
  --text-xl: 1.25rem;  /* 20 */  --text-2xl: 1.5rem;  /* 24 */
  --text-3xl: 1.875rem;/* 30 */  --text-4xl: 2.25rem; /* 36 */
  --text-5xl: 3rem;    /* 48 */  --text-6xl: 3.75rem; /* 60 */
  --text-7xl: 4.5rem;  /* 72 */

  --weight-normal: 400; --weight-medium: 500; --weight-bold: 600; /* or 700 */
  --leading-tight: 1.25;  /* large headings (1 is fine for very large) */
  --leading-normal: 1.5;  /* body */
  --leading-loose: 1.75;  /* small or wide text */
  --measure: 65ch;        /* paragraph max-width, ~45–75 chars */

  --font-ui: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Noto Sans",
             Ubuntu, Cantarell, "Helvetica Neue", sans-serif;

  /* Greys: cool-tinted, saturation rises toward the extremes */
  --grey-900: hsl(210 24% 16%);  /* darkest text, not #000 */
  --grey-800: hsl(209 20% 25%);
  --grey-700: hsl(209 15% 35%);  /* secondary text on white */
  --grey-600: hsl(209 12% 45%);
  --grey-500: hsl(210 10% 58%);  /* tertiary text, icons */
  --grey-400: hsl(211 13% 72%);
  --grey-300: hsl(210 16% 82%);  /* borders */
  --grey-200: hsl(214 15% 91%);
  --grey-100: hsl(216 33% 97%);  /* off-white app background */

  /* Primary: 500 = button background; 900 = text on 100 tint */
  --primary-900: hsl(221 72% 22%);
  --primary-800: hsl(221 68% 30%);
  --primary-700: hsl(221 63% 38%);
  --primary-600: hsl(221 62% 46%);
  --primary-500: hsl(221 70% 55%);
  --primary-400: hsl(221 80% 66%);
  --primary-300: hsl(221 88% 77%);
  --primary-200: hsl(221 95% 87%);
  --primary-100: hsl(221 100% 95%);

  /* Semantic accents: build full 100–900 scales the same way as needed */
  --red-100: hsl(0 100% 95%);   --red-500: hsl(0 72% 51%);   --red-900: hsl(0 70% 25%);
  --yellow-100: hsl(48 100% 94%); --yellow-500: hsl(42 95% 50%); --yellow-900: hsl(28 80% 26%); /* hue rotates toward orange as it darkens */
  --green-100: hsl(140 70% 94%); --green-500: hsl(145 60% 40%); --green-900: hsl(150 65% 18%);

  /* Elevation: 5 levels, each a soft large shadow + a tight dark shadow;
     the tight part fades as elevation rises */
  --shadow-1: 0 1px 3px hsl(0 0% 0% / .12), 0 1px 2px hsl(0 0% 0% / .24);   /* buttons */
  --shadow-2: 0 3px 6px hsl(0 0% 0% / .15), 0 2px 4px hsl(0 0% 0% / .12);   /* cards */
  --shadow-3: 0 10px 20px hsl(0 0% 0% / .15), 0 3px 6px hsl(0 0% 0% / .10); /* dropdowns */
  --shadow-4: 0 15px 25px hsl(0 0% 0% / .15), 0 5px 10px hsl(0 0% 0% / .05);/* popovers */
  --shadow-5: 0 20px 40px hsl(0 0% 0% / .20);                                /* modals */

  /* Radius: pick ONE family for the personality (formal 0 / neutral 4px / playful 12px+) */
  --radius-sm: 4px; --radius-md: 6px; --radius-lg: 8px; --radius-full: 9999px;
}
```

## Common recipes

```css
/* Raised button: lighter top edge + small sharp shadow below */
.btn-primary {
  background: var(--primary-500); color: white;
  box-shadow: inset 0 1px 0 var(--primary-400), var(--shadow-1);
  padding: var(--space-3) var(--space-5); font-weight: var(--weight-bold);
}
.btn-primary:active { box-shadow: inset 0 1px 0 var(--primary-400); } /* pressed in */
.btn-secondary { background: var(--primary-100); color: var(--primary-800); }
.btn-tertiary  { background: none; color: var(--primary-700); text-decoration: underline; }

/* Inset input: dark inner shadow at top */
.input { background: white; border: 1px solid var(--grey-300);
         box-shadow: inset 0 2px 2px hsl(0 0% 0% / .05); }

/* Alert: flipped contrast + accent border */
.alert { background: var(--primary-100); color: var(--primary-900);
         border-left: 4px solid var(--primary-500); padding: var(--space-4); }

/* User-uploaded image */
.avatar { width: 48px; aspect-ratio: 1; object-fit: cover; border-radius: var(--radius-full);
          box-shadow: inset 0 0 0 1px hsl(0 0% 0% / .1); } /* put on a wrapper; inset shadows don't render on <img> */

/* Readable text over a hero image */
.hero { background: linear-gradient(hsl(0 0% 0% / .5), hsl(0 0% 0% / .5)), url(hero.jpg) center/cover; }
.hero h1 { text-shadow: 0 0 40px hsl(0 0% 0% / .5); }

/* All-caps label */
.eyebrow { text-transform: uppercase; letter-spacing: .05em; font-size: var(--text-xs);
           color: var(--grey-600); font-weight: var(--weight-bold); }
/* Large headline tracking */
.display { font-size: var(--text-5xl); line-height: 1.1; letter-spacing: -.02em; }
```
