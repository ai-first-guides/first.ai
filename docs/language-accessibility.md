# Language & Accessibility

AI and assistive technologies both rely on **clear language signals** and **semantic markup** to understand your content.  
Defining language, structure, and accessibility metadata helps ensure that your website can be read, summarized, and cited correctly — by both humans and AI.

---

## 1) Declare language at every level

Always declare the **language of your page** in the `<html>` tag.  
If your content includes other languages inside, mark them with inline `lang` attributes.

```html
<html lang="en">
  <body>
    <p>Welcome to the AI-first Web guide.</p>
    <p><span lang="es">Bienvenido</span> and <span lang="zh">欢迎</span>!</p>
  </body>
</html>
```

✅ Why it matters
 - AI uses language tags to match users’ language preferences.
 - Screen readers choose correct pronunciation and reading rules.
 - Multilingual assistants can serve the right translation or voice.

## 2) Use hreflang for alternate language versions

Each translated page should reference all its siblings in the <head> section:
```html
<link rel="alternate" hreflang="en" href="https://example.com/en/guide">
<link rel="alternate" hreflang="es" href="https://example.com/es/guide">
<link rel="alternate" hreflang="zh" href="https://example.com/zh/guide">
<link rel="alternate" hreflang="x-default" href="https://example.com/guide">
```
💡 Tip:
`hreflang` helps AI and search engines treat all language versions as one conceptual document, rather than duplicates.
---

## 3) How AI chooses citations by language

When AI assistants search and quote information, they prefer sources written in the same language as the user’s query.
If your page declares its language properly (lang="en", lang="es", etc.) and links all translations with hreflang, AI can directly select and cite the correct version — instead of translating or skipping it.

If your site has multiple language versions, each correctly tagged:
 - AI will quote the exact version that matches the user’s language (e.g. a Spanish query → your Spanish text).
 - Your site gains visibility across multiple AI markets — one document, many entry points.
 - Assistants treat your domain as a verified multilingual source, not an auto-translated one.

If your site lacks language markup or translations:
 - AI may still use your text, but it will machine-translate it silently.
 - The citation might point to another source in the user’s language instead of yours.
 - You lose authorship visibility — your ideas appear, but your link does not.

If you only publish in one language:
 - Still declare that language in <html lang="...">.
 - Optionally note that your content targets global readers.
 - Consider short English summaries — English is often AI’s fallback citation language.

> In short: AI assistants quote what they can understand natively.
The clearer your language structure, the higher your chance to be the cited source, not just the translated one.

## 4) Declaring global intent (JSON-LD example)

Even if your site currently uses only one language, you can still declare that it’s intended for a global audience.
This helps AI include it in multilingual results and prevents language-based exclusion.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "AI-Readable Web Design Principles",
  "inLanguage": "en",
  "intendedAudience": {
    "@type": "Audience",
    "audienceType": "Global readers",
    "geographicArea": {
      "@type": "Place",
      "name": "Worldwide"
    }
  },
  "about": "Guidelines for creating websites understandable by AI systems across languages.",
  "author": {
    "@type": "Person",
    "name": "Michal Kuritka"
  },
  "publisher": {
    "@type": "Organization",
    "name": "AI-First Project",
    "url": "https://first.ai"
  },
  "datePublished": "2025-11-07"
}
</script>
```

**What this does**
 - inLanguage declares the actual written language.
 - intendedAudience signals that the page targets global readers.
 - geographicArea helps AI understand that the content is relevant worldwide.

> This is useful for technical or educational content that uses English as a universal medium — it keeps your pages visible even when users ask questions in other languages.

## 5) Accessibility landmarks (ARIA roles)

Use ARIA landmarks to describe key regions of your page.
They help both AI and assistive technologies understand layout and navigation.

| Element    | Default role    | When to add `aria-label`                        |
| ---------- | --------------- | ----------------------------------------------- |
| `<header>` | `banner`        | When multiple headers exist                     |
| `<nav>`    | `navigation`    | To specify type, e.g. `aria-label="Pagination"` |
| `<main>`   | `main`          | Only one per page                               |
| `<aside>`  | `complementary` | When summarizing or offering context            |
| `<footer>` | `contentinfo`   | For global or section footers                   |

```html
<nav aria-label="Main navigation">
  <ul>
    <li><a href="/docs/">Docs</a></li>
    <li><a href="/about/">About</a></li>
    <li><a href="/contact/">Contact</a></li>
  </ul>
</nav>
```

## 6) Labels and descriptions

Interactive elements (forms, buttons, inputs) must always have visible and programmatic labels.
```html
<label for="email">Email address</label>
<input id="email" name="email" type="email" autocomplete="email" placeholder="you@example.com">
```

### Best practices
 - Match <label for> and id.
 - Avoid placeholder-only labels.
 - Use aria-describedby for help text.

## 7) Contrast and clarity

AI-powered visual summarizers and accessibility tools rely on visual clarity and color contrast.
 - Text vs. background: 4.5:1 (WCAG AA)
 - Large text (≥18px or bold ≥14px): 3:1

**Tools:**
 - Contrast Checker
 - WAVE Accessibility Tool
> If your content becomes unreadable when CSS or JS is disabled, AI likely can’t interpret it either.

## 8) Captions and transcripts for media

Audio and video need text alternatives — AI often cannot parse sound, but it can process transcripts.
```html
<figure>
  <video controls src="/media/intro.mp4"></video>
  <figcaption>
    Introduction video explaining the principles of the AI-first web.
    Transcript available at <a href="/docs/transcripts/intro">/docs/transcripts/intro</a>.
  </figcaption>
</figure>
```

## 10) Quick checklist

 - [ ] `<html lang="...">` declared.
 - [ ] hreflang links connect language versions.
 - [ ] Multilingual intent defined (intendedAudience).
 - [ ] Semantic landmarks (header, nav, main, footer).
 - [ ] Input labels connected and descriptive.
 - [ ] Text and background contrast sufficient.
 - [ ] Captions or transcripts for media.
 - [ ] Validated with screen reader and AI crawler.

---

**Next:** see [Images & captions](./images-captions.md) to learn how to describe visual information for AI and accessibility tools.
