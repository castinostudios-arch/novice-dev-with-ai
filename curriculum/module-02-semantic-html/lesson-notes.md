# Module 2 — Semantic HTML5: Lesson Notes

**Prerequisites:** Module 1 milestone complete (boilerplate from memory)
**Read before:** Opening VS Code today

---

## Concept 1 — What is Semantic HTML?

"Semantic" means **meaningful**. A semantic HTML element describes what the content IS, not just how it looks.

Compare:
```html
<div class="nav">...</div>     <!-- What is this? A div. That's all we know. -->
<nav>...</nav>                 <!-- This is navigation. Everyone knows. -->
```

The browser, screen readers, search engines, and other developers all understand `<nav>`.
A `<div>` is just an empty container — it means nothing by itself.

**Why it matters:**
- Screen readers announce landmarks to blind users: "Navigation region, Main region"
- Search engines rank pages that use headings and semantic structure correctly
- Your code is easier to read and maintain
- Accessibility is not optional — it is correct HTML

---

## Concept 2 — Page Landmark Elements

These are the "regions" of a page. Every page should have most of these:

```html
<body>

  <!-- 1. Site header — logo, site name, top-level navigation -->
  <header>
    <h1>My Portfolio</h1>
    <nav>
      <a href="#about">About</a>
      <a href="#projects">Projects</a>
    </nav>
  </header>

  <!-- 2. Main content — ONE per page -->
  <main>

    <!-- 3. Section — thematic group of content -->
    <section id="about">
      <h2>About Me</h2>
      <p>I am a web developer learning HTML and CSS.</p>
    </section>

    <!-- 4. Article — standalone, redistributable content -->
    <article>
      <h2>Project: My First Website</h2>
      <p>Built with HTML5 and CSS3 during this course.</p>
    </article>

    <!-- 5. Aside — supplementary content, related but not main -->
    <aside>
      <h2>Quick Links</h2>
      <a href="https://github.com">GitHub</a>
    </aside>

  </main>

  <!-- 6. Footer — copyright, secondary links, contact -->
  <footer>
    <p>&copy; 2026 My Name. All rights reserved.</p>
  </footer>

</body>
```

**Element guide:**

| Element | Meaning | Use when... |
|---|---|---|
| `<header>` | Page or section header | Site banner, logo area, page intro |
| `<nav>` | Navigation links | Main menu, breadcrumbs, pagination |
| `<main>` | Primary content | The main point of the page (ONE only) |
| `<section>` | Thematic group | Grouping related content with a heading |
| `<article>` | Standalone content | Blog post, news item, product card |
| `<aside>` | Related but supplementary | Sidebar, callout box, related links |
| `<footer>` | Page or section footer | Copyright, contact, site links |

---

## Concept 3 — Text Elements

### Headings — Document Outline
```html
<h1>Page Title</h1>         <!-- ONE per page — the top-level topic -->
  <h2>Major Section</h2>    <!-- Main sections of the page -->
    <h3>Sub-section</h3>    <!-- Sub-topics within a section -->
      <h4>Detail</h4>       <!-- Rarely needed for beginners -->
```

Think of headings as a table of contents for your page.
Screen readers let users jump between headings to navigate.

### Paragraphs and Emphasis
```html
<p>This is a paragraph of text.</p>

<p>Use <strong>strong</strong> for important text — screen readers stress it.</p>
<p>Use <em>emphasis</em> for stressed text — screen readers change tone.</p>

<!-- NOT these — they are visual only, not semantic -->
<b>bold</b>    <!-- no meaning — just bold -->
<i>italic</i>  <!-- no meaning — just italic -->
```

### Blockquote and Cite
```html
<blockquote>
  <p>"First, solve the problem. Then, write the code."</p>
  <cite>— John Johnson</cite>
</blockquote>
```

---

## Concept 4 — Lists

### Unordered List (no sequence matters)
```html
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>
```

### Ordered List (sequence matters)
```html
<ol>
  <li>Open VS Code</li>
  <li>Create index.html</li>
  <li>Type the boilerplate</li>
  <li>Open with Live Server</li>
</ol>
```

### Description List (term + definition pairs)
```html
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language — the structure of a webpage</dd>
  <dt>CSS</dt>
  <dd>Cascading Style Sheets — the appearance of a webpage</dd>
</dl>
```

---

## Concept 5 — Links

```html
<!-- Internal link (same site) — relative path -->
<a href="/about">About me</a>
<a href="#projects">Jump to projects section</a>

<!-- External link (different site) — always add target and rel -->
<a href="https://github.com" target="_blank" rel="noopener noreferrer">
  My GitHub Profile
</a>
```

**Link text rules:**
- Must describe the destination: "View my portfolio" ✅
- Must NOT be generic: "Click here" ❌ / "Read more" ❌
- Screen reader users hear links in isolation — make each one make sense alone

---

## Concept 6 — Images

```html
<!-- Meaningful image — describe it -->
<img
  src="images/profile.jpg"
  alt="Amara smiling at a laptop in a cafe"
  width="300"
  height="300"
>

<!-- Decorative image — empty alt so screen readers skip it -->
<img src="images/wave-divider.png" alt="">
```

**Alt text guide:**
- Describe what you see in 1–2 sentences
- Do NOT start with "Image of" or "Photo of" — screen readers say "image" already
- For decorative images (backgrounds, dividers): `alt=""`

---

## Concept 7 — Forms

Forms are the most accessibility-critical HTML. Every control needs a label.

```html
<form action="/contact" method="POST">

  <!-- Text input with label -->
  <label for="name">Full name</label>
  <input type="text" id="name" name="name" required>

  <!-- Email input -->
  <label for="email">Email address</label>
  <input type="email" id="email" name="email" required>

  <!-- Textarea -->
  <label for="message">Message</label>
  <textarea id="message" name="message" rows="5"></textarea>

  <!-- Select dropdown -->
  <label for="topic">Topic</label>
  <select id="topic" name="topic">
    <option value="">Choose a topic</option>
    <option value="html">HTML question</option>
    <option value="css">CSS question</option>
  </select>

  <!-- Submit button -->
  <button type="submit">Send message</button>

</form>
```

**Form rules:**
- Every `<input>` needs a `<label>` linked by matching `for` and `id`
- `placeholder` is NOT a label — it disappears when you type
- Use `<button type="submit">` not `<input type="submit">`
- Use `required` attribute on mandatory fields

---

## Common Mistakes

| Mistake | Fix |
|---|---|
| Using `<div>` for navigation | Replace with `<nav>` |
| Multiple `<h1>` elements | Only ONE `<h1>` per page |
| Skipping heading levels (h1 → h3) | Always h1 → h2 → h3 in order |
| Missing `alt` on images | Every meaningful image needs `alt` |
| "Click here" link text | Describe the destination |
| Input without `<label>` | Always link label via `for`/`id` |
| Using `<b>` for importance | Use `<strong>` |
| Using `<i>` for emphasis | Use `<em>` |

---

## Exercises

### Exercise 2-A — Page Regions (Guided)
Build a 4-region page for a fictional bakery called "Sunshine Bakery":
- `<header>` with the bakery name as `<h1>` and a `<nav>` with 3 links
- `<main>` containing two `<section>` elements: "Our Story" and "Our Menu"
- `<footer>` with "© 2026 Sunshine Bakery"
- Zero `<div>` elements allowed

### Exercise 2-B — Semantic Text (Semi-guided)
Add to your bakery page:
- An `<article>` inside the "Our Story" section
- An unordered `<ul>` list of 5 menu items inside "Our Menu"
- At least one `<strong>` and one `<em>` used correctly
- One `<blockquote>` with a fictional customer testimonial

### Exercise 2-C — Links and Images (Challenge)
- Add a real image (find a free one at https://unsplash.com) with proper `alt` text
- Add 3 external links that open in a new tab with correct `rel` attribute
- Validate at https://validator.w3.org — zero errors

### Exercise 2-D — Contact Form (Challenge)
Add a contact form to your bakery page with:
- Full name field (text)
- Email field (email type)
- Message textarea
- A topic dropdown with 3 options
- Submit button
- All inputs linked to labels — validated with WAVE: https://wave.webaim.org

---

## Milestone Assessment

**Requirement to advance to Module 3:**

Submit a Pull Request with:
- A complete 4-region page (header, nav, main, footer)
- Zero `<div>` elements
- At least one image with descriptive `alt` text
- At least one link with descriptive text (no "click here")
- HTML validator: zero errors
- WAVE accessibility tool: zero errors
