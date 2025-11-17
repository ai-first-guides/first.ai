# AI-first Principles


The core idea behind AI-first is the growing shift in user behavior — more people now seek information directly from AI assistants rather than by browsing traditional websites.
The goal of this project is to define clear web guidelines that ensure content remains visible, citable, and accessible through AI assistants, not just via the browser.

AI-first web design means building websites that are **understandable, interpretable, and citable by AI systems** — not only viewable by humans.

It’s a shift from visual presentation to **semantic clarity**, **structured meaning**, and **machine readability**.  
Just as accessibility made the web inclusive for people, AI-first design makes it understandable for artificial intelligence.


## Why It Matters

The web is no longer consumed only by humans.  
AI assistants like ChatGPT, Perplexity, and Gemini now interpret billions of pages to answer questions, generate summaries, and cite sources.

However, most of today’s web is:
- overloaded with JavaScript,
- bloated with tracking scripts,
- and poor in structure or context.

AI-first design aims to reverse this trend — making the web readable again.

## Core Principles

### 1. Semantics over styling
Use native, meaningful HTML elements (`header`, `main`, `article`, `section`, `nav`, `footer`) instead of endless `<div>` and `<span>` wrappers.  
Structure should convey meaning even without CSS or JavaScript.

### 2. Content over decoration
Focus on the message, not marketing language or design gimmicks. 
AI assistants prioritize clarity, context, and source credibility — not animation or layout.

### 3. Machine-readable metadata
Use structured data (JSON-LD, microdata) to describe entities — articles, authors, products, events.  
This helps AI connect your content to real-world concepts and cite it correctly.

### 4. Multilingual and accessible
Add `lang` attributes, `hreflang` links, and clear labels.  
What improves accessibility for people also improves interpretability for AI.

### 5. Minimalism and transparency
Remove unnecessary code, inline styles, and frameworks.  
Keep the DOM simple. Every extra layer is another barrier for crawlers and AI parsers.

### 6. Ethical openness
Allow AI crawlers to read your site responsibly (`robots.txt`).  
Respect attribution, privacy, and licensing.  
The AI-first web should be open, but fair.

## Practical Outcome

When AI reads your page, it should be able to answer:

1. *What is this page about?*
2. *Who wrote it?*
3. *When was it published or updated?*
4. *What entities (people, products, ideas) does it describe?*
5. *Can it be safely cited or quoted?*

If those questions can be answered directly from your markup, your site is AI-ready.

---

**Next:** see [HTML structure for AI](./html-structure.md) to learn how to express meaning through semantics instead of visual layout.
