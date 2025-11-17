# Metadata (JSON-LD)
Structured data makes your content machine-readable and citable.
While HTML gives AI the human-facing meaning, JSON-LD expresses the same facts in a form that AI models and search systems can parse directly.

## 1) What is JSON-LD?

**JSON-LD (JavaScript Object Notation for Linked Data)** is a standard format for embedding metadata in web pages.
It uses a `<script type="application/ld+json">` tag to describe the entities on the page — articles, products, people, organizations, events, etc.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "AI-First Web Design Principles",
  "author": {
    "@type": "Person",
    "name": "Michal Kuritka"
  },
  "datePublished": "2025-11-07",
  "inLanguage": "en",
  "about": "AI-readable website design and metadata best practices",
  "publisher": {
    "@type": "Organization",
    "name": "AI-First Project",
    "url": "https://first.ai"
  }
}
</script>
```

💡 **Tip:**
Everything in the JSON-LD must reflect real content visible on the page.
If AI or users can’t see it, don’t describe it as if it exists.

## 2) Why it matters
 - AI assistants and search engines use JSON-LD to extract facts, authors, topics, and relationships.
 - Proper metadata increases the chance your page will be cited as a trusted source.
 - JSON-LD allows for multilingual references, canonical versions, and verifiable timestamps.
 > Think of JSON-LD as the “structured mirror” of your HTML — the factual summary AI reads first.

## 3) Common schema types

| Type           | Purpose                                  | Example use                 |
| -------------- | ---------------------------------------- | --------------------------- |
| `Article`      | Blog post, documentation page, news item | `/docs/html-structure.md`   |
| `Product`      | Goods, software, physical items          | product pages, app listings |
| `Person`       | Authors, creators, team members          | “About” pages               |
| `Organization` | Company, project, or institution         | site-wide metadata          |
| `Event`        | Conferences, launches, meetups           | announcements or news       |
| `FAQPage`      | Common questions and answers             | help or support pages       |

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Ristretto Grinder",
  "brand": "AI-Brew",
  "description": "Compact coffee grinder with precision stainless burrs.",
  "sku": "GR-201",
  "offers": {
    "@type": "Offer",
    "priceCurrency": "USD",
    "price": "129.99",
    "availability": "https://schema.org/InStock"
  }
}
</script>
```

## 4) Multilingual metadata

When your page has content in multiple languages, describe language variants explicitly:
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": {
    "en": "AI-Readable Web Design",
    "zh": "可被人工智能读取的网页设计",
    "es": "Diseño web legible por IA"
  },
  "inLanguage": ["en", "zh", "es"],
  "url": "https://example.com/ai-readable-web-design",
  "alternateName": {
    "en": "How to make your website understandable for AI",
    "zh": "让网站更容易被人工智能理解",
    "es": "Cómo hacer que tu sitio web sea comprensible para la IA"
  },
  "datePublished": "2025-11-07",
  "author": {
    "@type": "Person",
    "name": "Michal Kuritka"
  },
  "publisher": {
    "@type": "Organization",
    "name": "AI-First Project",
    "url": "https://first.ai"
  }
}
</script>
```
This helps AI assistants choose which version to quote or present to the user.

💡 Tip:
- Always include the inLanguage array and make sure each version uses the proper IETF language tag
(`en`, `zh`, `es`, `fr`, etc.).
- Link each language variant using `<link rel="alternate" hreflang="...">` in your HTML `<head>` — this helps both AI and search engines connect the versions.

## 5) Connect JSON-LD with HTML IDs

If your page contains definitions, quotes, or data with `id` anchors, you can reference them directly in JSON-LD.

```html
<p id="def-ai-first">
  <strong>AI-first website</strong> — a site designed so that its meaning is clear to both humans and AI.
</p>

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "DefinedTerm",
  "@id": "#def-ai-first",
  "name": "AI-first website",
  "description": "A site designed so that its meaning is clear to both humans and AI."
}
</script>
```
That link (`@id`) helps AI models map textual and structured meaning together.

## 6) Validation and testing

Before publishing, always validate your JSON-LD:

[Google Rich Results Test](https://search.google.com/test/rich-results)
[Schema.org Validator](https://validator.schema.org/)
[JSON-LD Playground](https://json-ld.org/playground/)

Errors in syntax, context, or type hierarchy can make your metadata invisible to AI parsers.

---

**Next:** see [Language & accessibility](./language-accessibility.md) to ensure your content is readable and correctly cited across languages.
