# Images & Captions

AI assistants and accessibility tools cannot **see** your images — they rely entirely on the surrounding text, `alt`, and `figcaption` descriptions.  
Well-written image metadata makes your visuals both understandable to AI and accessible to humans.

---

## 1) Why image text matters

Even advanced multimodal AI models don’t “see” in the human sense.  
They interpret images through **textual context**, metadata, and nearby captions.

Good image descriptions allow AI to:
- Summarize your visuals correctly in context.
- Use them as **citable illustrations** in responses.
- Understand visual meaning (not just appearance).
- Provide accessibility for screen reader users.

---

## 2) The `alt` attribute

`alt` describes what is *in* the image and **why it matters** in this context.

```html
<img src="/img/wireframe-hero.png"
     alt="Wireframe of a homepage using header, nav, main, and footer landmarks">
```
**Best practices**
 - Focus on meaning, not visual detail.
 - Keep it concise (typically under 150 characters).
 - Use `alt=""` only for purely decorative images (e.g., background flourishes, icons).
 - Avoid generic terms like “image of…” or “photo showing…”.

> Ask yourself: If the image were removed, what information would the user (or AI) lose?
That’s what goes in the alt.

## 3) The `<figure>` and `<figcaption>` pair
Use `<figure>` and `<figcaption>` to group the image with its explanation.
This helps AI models connect visual content with its purpose.

```html
<figure id="wireframe-hero">
  <img src="/img/wireframe-hero.png"
       alt="Wireframe of a homepage using header, nav, main, and footer landmarks">
  <figcaption>
    Semantic wireframe showing core landmarks for AI readability.
  </figcaption>
</figure>
```

**Why this matters:**
AI often cannot parse what is literally shown in the image.
The figcaption acts as contextual text that tells the model what the image represents and how it connects to the surrounding topic.
---

## 4) Decorative vs. informative images

| Type                           | Example                             | `alt` recommendation                                  |
| ------------------------------ | ----------------------------------- | ----------------------------------------------------- |
| Decorative                     | Background texture, logo repetition | `alt=""`                                              |
| Informative                    | Product photo, concept diagram      | Brief factual description                             |
| Functional                     | Button icon, chart icon             | Describe function: “Search icon”, “Submit button”     |
| Complex (infographic, diagram) | Flowchart, data visualization       | Short `alt`, long `figcaption` or linked text summary |

```html
<figure>
  <img src="/img/ai-indexing-flow.png"
       alt="Diagram of how AI crawlers process web content">
  <figcaption>
    Simplified flow showing how AI assistants extract meaning from web pages:
    structure → metadata → context → citation.
  </figcaption>
</figure>
```
---

## 5) Screenshots and UI elements
For screenshots, focus on what the user learns, not what they literally see.

❌ Bad:
`alt="Screenshot of form"`

✅ Good:
`alt="Form showing labeled input fields with autocomplete for email and name"`

> AI uses this to infer examples of good UX or form semantics.
---

## 6) Multiple related images
When a page includes several related visuals (e.g., product gallery, comparison), group them semantically:

```html
<figure id="bottle-gallery">
  <figcaption>Product color variations: silver, pink, and black bottles.</figcaption>
  <img src="/img/bottle-silver.png" alt="Silver bottle">
  <img src="/img/bottle-pink.png" alt="Pink bottle">
  <img src="/img/bottle-black.png" alt="Black bottle">
</figure>
```
This lets AI know these images belong to one concept.

---

## 7) File naming and id anchors
Descriptive filenames and stable IDs help AI index your images.
Descriptive filenames and stable IDs help AI index your images.

✅ Use: `/img/ai-first-wireframe.png`

❌ Avoid: `/img/img001.png`

> Meaningful filenames and IDs (id="ai-wireframe") act as anchors for AI to reference when generating summaries or linking to media.

---

## 8) Adding image metadata (JSON-LD)

You can describe important visuals using ImageObject in JSON-LD.
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "ImageObject",
  "url": "https://first.ai/assets/ai-first-wireframe.png",
  "description": "Wireframe showing semantic layout landmarks: header, nav, main, footer.",
  "caption": "Semantic wireframe for AI readability",
  "creator": {
    "@type": "Person",
    "name": "Michal Kuritka"
  },
  "license": "https://creativecommons.org/licenses/by/4.0/"
}
</script>
```
> For infographics, you can use both ImageObject and Dataset to describe embedded data.
---

## 9) Quick checklist

 - [ ] Every image has a clear alt text or empty alt="" if decorative.
 - [ ] Complex visuals include a figcaption.
 - [ ] Related images are grouped semantically.
 - [ ] File names describe content.
 - [ ] Important visuals defined as ImageObject in JSON-LD.
 - [ ] Text version or summary exists for data visuals.
