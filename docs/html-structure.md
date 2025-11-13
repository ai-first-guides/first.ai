# HTML structure for AI
AI (and screen readers) rely on clear hierarchy, landmarks, and stable anchors.

## 1) Page skeleton (the meaningful minimum)
```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>AI-first Web: Quick Start</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <!-- Canonical URL helps AI pick the primary source -->
  <link rel="canonical" href="https://example.com/ai-first-quickstart">

  <!-- Hreflang for language variants -->
  <link rel="alternate" hreflang="en" href="https://example.com/en/ai-first-quickstart">
  <link rel="alternate" hreflang="cs" href="https://example.com/cs/ai-first-quickstart">

  <!-- JSON-LD placeholder (see metadata section for full patterns) -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Article",
    "headline": "AI-first Web: Quick Start",
    "inLanguage": "en"
  }
  </script>
</head>
<body>
  <header role="banner">
    <h1>AI-first Web: Quick Start</h1>
    <nav aria-label="Primary">
      <ul>
        <li><a href="/docs/">Docs</a></li>
        <li><a href="/docs/principles">Principles</a></li>
        <li><a href="/docs/content">Meaningful content</a></li>
      </ul>
    </nav>
  </header>

  <main id="main" role="main">
    <article aria-labelledby="title">
      <h2 id="title">Why structure matters</h2>
      <p>Clear semantics and stable anchors make your page understandable and citable.</p>

      <section aria-labelledby="benefits">
        <h3 id="benefits">Key benefits</h3>
        <ul>
          <li>Better AI understanding and citation</li>
          <li>Usable without JS/CSS</li>
          <li>Stable deep-link anchors</li>
        </ul>
      </section>
    </article>

    <aside aria-label="Summary">
      <h2>TL;DR</h2>
      <p>Use semantic tags, concise headings, and JSON-LD.</p>
    </aside>
  </main>

  <footer role="contentinfo">
    <p>&copy; 2025 Example</p>
  </footer>

  <!-- Progressive enhancement only -->
  <noscript>
    JavaScript is disabled; interactive features are simplified.
  </noscript>
</body>
</html>
```

#### Rules of thumb
 - One `<h1>` per page. Use h2–h4 for a consistent hierarchy.
 - Prefer `header`, `nav`, `main`, `article`, `section`, `aside`, `footer` over generic `<div>`.
 - Every section has a meaningful heading (optionally `aria-labelledby`).
 - Use stable anchors (`id`) for citations and deep links.
 - Expose critical content in the initial HTML or JSON-LD instead of fetching it via JavaScript.
---

## 2) Headings & hierarchy
```html
<main>
  <article>
    <h1>Guide to AI-readable Product Pages</h1>

    <section id="intro">
      <h2>Introduction</h2>
      <p>What “AI-readable” means in practice.</p>
    </section>

    <section id="data-model">
      <h2>Data model</h2>
      <h3>Required fields</h3>
      <ul>
        <li>name</li><li>brand</li><li>description</li><li>price</li>
      </ul>
      <h3>Optional fields</h3>
      <ul>
        <li>sku</li><li>gtin</li><li>aggregateRating</li>
      </ul>
    </section>

    <section id="faq">
      <h2>FAQ</h2>
      <h3>How should I handle variants?</h3>
      <p>Describe each variant explicitly and link to the canonical page.</p>
    </section>
  </article>
</main>
```
#### Tips
 - Headings should state what follows, not market it.
 - Don’t skip levels (`h2` → `h4` without `h3`). Skipping heading levels breaks the logical outline of the page.
   AI models like ChatGPT, Gemini, or Copilot build internal hierarchies from headings — if the structure is inconsistent, they may merge unrelated sections, skip content in summaries, or mislabel parts of the page.
   Screen readers also lose proper navigation, making it unclear where the user is in the document.
---

## 3) Navigation, breadcrumbs, sitemap

```html

<nav aria-label="Breadcrumb">
    <ol>
        <li><a href="/">Home</a></li>
        <li><a href="/docs/">Docs</a></li>
        <li aria-current="page">HTML structure for AI</li>
    </ol>
</nav>
```
- Breadcrumbs give context and hierarchy to AI.
- Maintain a `sitemap.xml` with important pages (don’t rely solely on auto-generation). A sitemap.xml file gives AI and crawlers a complete overview of your website’s structure.
  It lists all important pages, helping AI discover relationships, priorities, and update frequency — even without browsing your entire site.
---

## 4) Links & anchors (citeability > clickability)

```html
<p id="definition-ai-readable">
  <strong>AI-readable content</strong> means content that can be understood and cited by AI systems without executing JavaScript.
</p>
<p>
  Learn more in the <a href="#definition-ai-readable">definition of AI-readable content</a>.
</p>
```
Use short, stable id attributes for definitions, key paragraphs, or sections that may be referenced or cited by others.
A predictable, permanent id (like #definition-ai-readable) allows AI models, crawlers, and even humans to create deep links that always point to the same piece of conten

Anchor text should describe the target, not use generic phrases like “click here” or “read more.”
```html
<!-- ❌ Bad -->
<p>To learn more, <a href="#definition-ai-readable">click here</a>.</p>

<!-- ✅ Good -->
<p>See the <a href="#definition-ai-readable">definition of AI-readable content</a> for 
```
💡 Tip:
Descriptive links make your content easier to quote, summarize, and navigate — for both AI and accessibility tools.
---
## 5) Tables, lists, code
```html
<table>
  <caption>Minimum fields for Product</caption>
  <thead>
    <tr><th>Field</th><th>Type</th><th>Required</th></tr>
  </thead>
  <tbody>
    <tr><td>name</td><td>Text</td><td>Yes</td></tr>
    <tr><td>description</td><td>Text</td><td>Yes</td></tr>
    <tr><td>price</td><td>Number (currency)</td><td>Yes</td></tr>
  </tbody>
</table>

<pre><code class="language-json">{
  "name": "Ristretto Grinder",
  "price": 129.99,
  "currency": "EUR"
}</code></pre>
```
- `caption` gives a short, explicit title or context for the table — this is critical because AI and screen readers don’t “see” visual placement.
Without a caption, AI may not understand what the data describes (e.g., product specs vs. pricing table).
- `th` headers define column meaning and help AI correctly associate values in each row.
- Avoid using tables for layout or decoration — they pollute the document’s semantic outline.
- Wrap code in `<pre><code>` with an optional language class.
## 6) Images & captions (see the dedicated section for more)
```html
<figure id="wireframe-hero">
    <img src="/img/wireframe-hero.png"
         alt="Wireframe of a homepage showing header, nav, main, and footer landmarks.">
    <figcaption>Semantic wireframe illustrating the basic structure of an AI-readable layout.</figcaption>
</figure>
```
`alt` describes what is shown in the image and why it matters in this context.
Example: not just “wireframe”, but “wireframe of a homepage showing key landmarks”.

Use `alt=""` only for purely decorative images that convey no meaningful information.

`figcaption` adds the human meaning behind the image — explaining what the image represents or demonstrates.
AI models can’t always “see” or interpret the image itself, so the caption acts as a textual substitute that gives the same information in a form AI can understand and cite.

💡 Tip:
Together, `alt` and `figcaption` transform an image from a visual element into structured, interpretable information — something both AI and assistive technologies can reference or summarize just like text.
---
## 7) Pagination & related content
```html
<nav aria-label="Pagination">
  <ul>
    <li><a rel="prev" href="/docs/html-structure?page=1">Previous</a></li>
    <li aria-current="page">2</li>
    <li><a rel="next" href="/docs/html-structure?page=3">Next</a></li>
  </ul>
</nav>

<section aria-labelledby="related">
  <h2 id="related">Related</h2>
  <ul>
    <li><a href="/docs/metadata-jsonld">Metadata (JSON-LD)</a></li>
    <li><a href="/docs/content">Meaningful content</a></li>
  </ul>
</section>
```

`aria-label` helps provide meta information for elements that have no visible text — such as icons, navigation containers, or pagination blocks.
It tells AI and assistive technologies _what the element represents_, even if the user cannot “see” it directly.

This example shows two common navigational patterns that help both AI and accessibility tools understand page relationships:

 - **Pagination navigation** (`aria-label="Pagination"`) clearly identifies a group of links that move between pages.
The `aria-current="page"` attribute tells AI and screen readers which page number is active — in this case, page 2.

 - **Related content section** (`aria-labelledby="related"`) points AI to additional, contextually linked documents.
By connecting the section to the visible heading (`<h2 id="related">Related</h2>`), both humans and AI understand that the following list contains related topics rather than part of the main content.

💡 Tip:
Explicit structure like this improves how AI models build internal maps of your site — understanding which pages are connected and how users (or assistants) can navigate between them.
---
## 8) Progressive enhancement (JS is optional, not required)

```html
<button id="copy-anchor" data-target="#def-meaning">Copy link</button>

<script>
  // Keep JS optional: the page must remain usable without it.
  document.getElementById('copy-anchor')?.addEventListener('click', () => {
    const target = document.getElementById('copy-anchor').dataset.target;
    const url = location.origin + location.pathname + target;
    navigator.clipboard.writeText(url);
  });
</script>
```
- The page must work without JS.
- JS = enhancement (copy-to-clipboard, filters…), not the source of content.
- Avoid CSR-only SPA pages where HTML is empty until JS runs.
---
# 9) Form input types and metadata
Form fields carry built-in metadata that describes what kind of information they expect.
Browsers use it for validation, autofill, and keyboard optimization — and AI assistants can use the same metadata to understand form intent or generate structured data.
```html
<form action="/subscribe" method="post">
  <label for="email">Email address</label>
  <input id="email" name="email" type="email" placeholder="you@example.com" required>

  <label for="age">Age</label>
  <input id="age" name="age" type="number" min="1" max="120">

  <label for="message">Your message</label>
  <textarea id="message" name="message" placeholder="Write your note..."></textarea>

  <button type="submit">Send</button>
</form>
```
**Key points:**
- type attribute acts as semantic metadata (`email`, `url`, `number`, `tel`, `date`, `search`, etc.).
It tells browsers and AI what kind of data belongs in the field.
- **Validation and intent** — built-in types automatically enforce formatting rules (e.g. valid email syntax).
- **Accessibility and AI understanding** — structured inputs make it easier for AI to recognize the purpose of each field and to prefill or suggest values correctly.
- Add descriptive `label` and `placeholder` — these give both human and machine readers context about the data being requested.
- Use autocomplete when possible — it strengthens intent recognition for both AI and browsers:
```html
<input type="email" name="email" autocomplete="email">
<input type="tel" name="phone" autocomplete="tel">
<input type="given-name" name="firstName" autocomplete="given-name">
```
💡 Tip:
Think of each input field as a small, machine-readable contract: it tells AI what kind of value is expected and how it will be used.
---
## 10) Anti-patterns (avoid these)
- “Div soup” with no semantics (`<div class="h1">` instead of a real `<h1>`).
- Important text embedded as an image.
- **Infinite scroll** without page links.
- Gating core content behind modals/cookie walls without fallback.
- Obfuscated text (canvas, SVG without `title/desc`).
- Heavy JS/CSS bundles that block HTML from loading.
---
## 11) Quick checklist
- [ ] One meaningful `<h1>`; consistent `h2–h4`.
- [ ] Use `header/nav/main/article/section/aside/footer` appropriately.
- [ ] Stable `id` for definitions and key sections.
- [ ] `alt` + `figcaption` for significant images.
- [ ] Visible previous/next and related links.
- [ ] `canonical` + `hreflang` (if multilingual).
- [ ] Page makes sense without JS and CSS.
- [ ] JSON-LD present in `<head>` (see metadata section).
---
## 12) Starter template (copy–paste)
```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>{Page Title}</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="canonical" href="https://example.com/{slug}">
  <!-- <link rel="alternate" hreflang="cs" href="https://example.com/cs/{slug}"> -->

  <!-- JSON-LD: fill with real data per page -->
  <script type="application/ld+json">
  {
    "@context":"https://schema.org",
    "@type":"Article",
    "headline":"{Page Title}",
    "inLanguage":"en"
  }
  </script>
</head>
<body>
  <header role="banner">
    <h1>{Page Title}</h1>
    <nav aria-label="Primary">
      <ul>
        <li><a href="/docs/">Docs</a></li>
        <li><a href="/docs/principles">Principles</a></li>
        <li><a href="/docs/metadata-jsonld">Metadata</a></li>
      </ul>
    </nav>
  </header>

  <main id="main" role="main">
    <article>
      <section id="intro">
        <h2>Introduction</h2>
        <p>Brief, factual intro to the topic.</p>
      </section>

      <section id="core">
        <h2>Core ideas</h2>
        <ul>
          <li>Semantic tags</li>
          <li>Stable anchors</li>
          <li>Minimal JS</li>
        </ul>
      </section>
    </article>

    <aside aria-label="Summary">
      <h2>Summary</h2>
      <p>One-paragraph TL;DR for AI and humans.</p>
    </aside>

    <nav aria-label="Related">
      <h2>Related</h2>
      <ul>
        <li><a href="/docs/content">Meaningful content</a></li>
        <li><a href="/docs/metadata-jsonld">Metadata (JSON-LD)</a></li>
      </ul>
    </nav>
  </main>

  <footer role="contentinfo">
    <p>&copy; 2025 Example</p>
  </footer>
</body>
</html>
```
