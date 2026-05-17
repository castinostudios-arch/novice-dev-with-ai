# Module 3 — Introduction to CSS: Lesson Notes

**Prerequisites:** Module 2 milestone complete
**Read before:** Opening VS Code today

---

## Concept 1 — What is CSS and How Does It Connect?

CSS (Cascading Style Sheets) controls the **appearance** of your HTML.
HTML says what things ARE. CSS says what they LOOK LIKE.

**Step 1 — Create `style.css`** in the same folder as your HTML.

**Step 2 — Link it inside `<head>`:**
```html
<head>
  <link rel="stylesheet" href="style.css">
</head>
```

Without this link, your CSS file does nothing. The browser won't find it.

**CSS syntax — one rule looks like this:**
```css
selector {
  property: value;
  property: value;
}
```

- `selector` — which element to style (`p`, `.card`, `h1`)
- `property` — what to change (`color`, `font-size`, `margin`)
- `value` — what to change it to (`red`, `1.5rem`, `2rem`)

---

## Concept 2 — Selectors

```css
/* Element selector — targets ALL <p> tags */
p {
  color: #1e293b;
}

/* Class selector — targets elements with class="card" */
.card {
  background-color: white;
  padding: 1.5rem;
}

/* ID selector — targets ONE element with id="hero" */
/* Use sparingly — IDs should mainly be for JavaScript */
#hero {
  background-color: #2563eb;
}

/* Descendant selector — targets <a> inside <nav> */
nav a {
  color: white;
  text-decoration: none;
}
```

**Specificity — when rules conflict, the more specific one wins:**
```
ID (#) = 100 points
class (.) = 10 points
element (p, h1) = 1 point

The rule with more points wins.
```

---

## Concept 3 — The Box Model (Most Important Concept in CSS)

Every HTML element is a rectangular box. From inside out:

```
┌─────────────────────────────────────┐
│             MARGIN                  │  pushes other elements away
│   ┌─────────────────────────────┐   │
│   │           BORDER            │   │  the visible edge
│   │   ┌─────────────────────┐   │   │
│   │   │       PADDING       │   │   │  space inside, between content and border
│   │   │   ┌─────────────┐   │   │   │
│   │   │   │   CONTENT   │   │   │   │  your text or image
│   │   │   └─────────────┘   │   │   │
│   │   └─────────────────────┘   │   │
│   └─────────────────────────────┘   │
└─────────────────────────────────────┘
```

```css
.card {
  /* Content size */
  width: 300px;
  height: 200px;

  /* Padding — space INSIDE the border */
  padding: 1.5rem;               /* all 4 sides */
  padding: 1rem 2rem;            /* top/bottom left/right */
  padding-top: 1rem;             /* individual sides */

  /* Border */
  border: 2px solid #e2e8f0;
  border-radius: 8px;            /* rounded corners */

  /* Margin — space OUTSIDE the border */
  margin: 0 auto;                /* center horizontally */
  margin-bottom: 1.5rem;
}
```

**The essential reset — put this at the top of every CSS file:**
```css
*, *::before, *::after {
  box-sizing: border-box;  /* padding stays INSIDE the width */
  margin: 0;
  padding: 0;
}
```

Without `box-sizing: border-box`, padding adds to the total width — confusing.
With it, `width: 300px` means the total box is always 300px, padding included.

**Inspect it:** Open DevTools (F12) → click any element → see the box model diagram.

---

## Concept 4 — Typography

```css
body {
  /* Font family — always provide fallbacks */
  font-family: 'Inter', system-ui, sans-serif;

  /* Font size — use rem (relative to browser default, usually 16px) */
  font-size: 1rem;       /* = 16px */

  /* Line height — space between lines (unitless = relative to font-size) */
  line-height: 1.6;

  /* Text color */
  color: #1e293b;
}

h1 { font-size: 2.5rem; font-weight: 700; }
h2 { font-size: 1.75rem; font-weight: 600; }
h3 { font-size: 1.25rem; font-weight: 600; }

p  { margin-bottom: 1rem; }

a  {
  color: #2563eb;
  text-decoration: underline;
}
a:hover {
  color: #1d4ed8;
}
```

**Why `rem` not `px` for fonts?**
`px` is fixed. If a user increases their browser font size for accessibility,
`px` values ignore that. `rem` scales with the user's preference.

---

## Concept 5 — Colors

```css
/* Named colors — easy but limited */
color: red;
color: navy;

/* Hex — most common */
color: #2563eb;    /* #RRGGBB — 00 = none, ff = full */
color: #fff;       /* shorthand for #ffffff */

/* RGB */
color: rgb(37, 99, 235);

/* HSL — most intuitive for designers */
color: hsl(221, 83%, 53%);
/*          ↑     ↑    ↑
         hue  saturation lightness  */

/* Transparency */
color: rgba(37, 99, 235, 0.5);   /* 50% transparent */
color: hsl(221 83% 53% / 0.5);
```

**Tip:** Use HSL when you want to create color variations.
Change only the lightness to get darker/lighter versions of the same hue.

---

## Concept 6 — CSS Custom Properties (Variables)

Define once, use everywhere. Change in one place, updates everywhere.

```css
/* Define in :root so every element can use them */
:root {
  --color-primary:    #2563eb;
  --color-text:       #1e293b;
  --color-text-muted: #64748b;
  --color-bg:         #f8fafc;
  --color-border:     #e2e8f0;

  --space-sm:  0.5rem;
  --space-md:  1rem;
  --space-lg:  1.5rem;
  --space-xl:  2rem;

  --radius-sm: 4px;
  --radius-md: 8px;
}

/* Use them anywhere in your CSS */
.card {
  background-color: var(--color-bg);
  color: var(--color-text);
  padding: var(--space-lg);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
}
```

---

## Concept 7 — The `display` Property

```css
/* block — takes full width, starts on new line */
/* Default for: div, p, h1-h6, section, article, etc. */
.block-element { display: block; }

/* inline — sits in line with text, width = content */
/* Default for: a, span, strong, em */
.inline-element { display: inline; }

/* inline-block — inline placement BUT accepts width/height/padding */
/* Useful for buttons, badges */
.badge {
  display: inline-block;
  padding: 0.25rem 0.75rem;
  border-radius: 4px;
}

/* none — hides the element completely (takes no space) */
.hidden { display: none; }
```

---

## Full Example — A Styled Card

```html
<!-- HTML -->
<article class="card">
  <h2 class="card__title">Module 1 Complete</h2>
  <p class="card__body">I learned the HTML boilerplate and built my first webpage.</p>
  <a href="#" class="card__link">View project</a>
</article>
```

```css
/* CSS */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

:root {
  --color-primary: #2563eb;
  --color-text: #1e293b;
  --color-bg: #ffffff;
  --color-border: #e2e8f0;
}

body {
  font-family: system-ui, sans-serif;
  font-size: 1rem;
  line-height: 1.6;
  color: var(--color-text);
  background: #f8fafc;
  padding: 2rem;
}

.card {
  background: var(--color-bg);
  border: 1px solid var(--color-border);
  border-radius: 8px;
  padding: 1.5rem;
  max-width: 400px;
}

.card__title {
  font-size: 1.25rem;
  margin-bottom: 0.5rem;
}

.card__body {
  color: #64748b;
  margin-bottom: 1rem;
}

.card__link {
  color: var(--color-primary);
  font-weight: 600;
  text-decoration: none;
}

.card__link:hover {
  text-decoration: underline;
}
```

---

## Exercises

### Exercise 3-A — Link CSS and Selectors
1. Create `style.css` linked to your Module 2 bakery page
2. Add the reset at the top
3. Style every `h1`, `h2`, and `p` element
4. Add a `.highlight` class to any element and style it differently

### Exercise 3-B — Box Model Inspector
1. Add a `.card` class to one `<article>` on your page
2. Style it with padding, border, and margin
3. Open DevTools → click your card → find the Box Model panel
4. Screenshot it and describe what you see in a comment in your CSS file

### Exercise 3-C — Typography + Colors
1. Add a Google Font to your page (https://fonts.google.com → "Get font" → copy the link tag)
2. Apply it to `body`
3. Define at least 4 CSS variables in `:root`
4. Use them throughout your CSS (no hardcoded hex values in properties)

### Exercise 3-D — Styled Full Page (Milestone Prep)
Style your bakery page completely from scratch. Requirements:
- CSS reset
- CSS variables for colors and spacing
- Custom typography (Google Font)
- Box model applied to at least 2 components
- External CSS only — CSS validator: zero errors

---

## Milestone Assessment

**Requirement to advance to Module 4:**

Submit a Pull Request with a fully styled page:
- CSS reset present
- CSS variables defined and used
- Custom font applied
- At least 2 card or box components styled with padding/border/margin
- Colors are consistent (using variables)
- CSS validator: zero errors
