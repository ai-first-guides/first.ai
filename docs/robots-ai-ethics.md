# robots.txt & AI Ethics

As AI assistants and search systems increasingly crawl the web, websites need a way to **control how automated agents access and reuse their content**.  
The `robots.txt` file and related headers define these permissions — technically and ethically.

---

## 1) Purpose of `robots.txt`

A `robots.txt` file at the root of your domain tells crawlers **which parts of your site they may access**.

Example:
```txt
User-agent: *
Disallow: /private/
Allow: /public/
Sitemap: https://example.com/sitemap.xml
```
**What it does**
 - `User-agent`: specifies the crawler (e.g., Googlebot, GPTBot).
 - `Disallow`: blocks paths from being crawled.
 - `Allow`: explicitly grants access.
 - `Sitemap`: provides the structured index of your content.

**AI relevance:**
AI crawlers (like OpenAI’s `GPTBot`, Anthropic’s `ClaudeBot`, or Google’s `Gemini`) check your `robots.txt` before reading or summarizing content.

---

# 2) Example with AI-specific bots

You can define policies for individual AI agents:
```txt
User-agent: GPTBot
Disallow: /drafts/
Allow: /docs/

User-agent: ClaudeBot
Disallow: /private/
Allow: /

User-agent: *
Disallow:
```

This setup:
 - Blocks AI bots from reading /drafts/.
 - Allows documentation to be cited and learned from.
 - Keeps everything else open for indexing.

> The file is advisory — ethical AI crawlers respect it, but not all agents do.
---

## 3) Declaring AI access in HTML
While `robots.txt` controls crawler access at the domain level,
you can also declare access preferences per individual page using `<meta>` tags in the `<head>` section.
This helps AI systems understand whether a given page is meant to be indexed, summarized, or excluded.

```html
<head>
    <meta name="robots" content="index, follow">
    <meta name="ai-access" content="allow">
    <meta name="ai-policy" content="cite-source, no-train">
</head>
```
 - `robots="index, follow"` — standard instruction allowing normal search indexing.
 - `ai-access="allow"` — signals that AI assistants may read and reference this content.
 - `ai-policy="cite-source, no-train"` — optional convention to clarify that the page may be cited, but not used for model training.

These meta tags are **not yet formal standards**, but they are increasingly adopted as a transparent way to communicate intent to AI crawlers.

**Example — restrict AI-only access**
```html
<head>
  <meta name="robots" content="index, follow">
  <meta name="ai-access" content="deny">
  <meta name="ai-policy" content="no-summary, no-train">
</head>
```
This allows normal web indexing but tells AI crawlers not to read or summarize the page.

**Why use meta tags in addition to robots.txt**
 - **Granularity** — apply rules at the page or section level, not the whole domain.
 - **Transparency** — users and AI both see access intent directly in the HTML.
 - **Fallback** — if a crawler skips robots.txt, it still sees the signal inside the page.
 - **Consistency** — meta instructions can mirror your overall policy for easier maintenance.

**Recommended combo**

In practice, use both methods together:
**robots.txt**
```txt
User-agent: GPTBot
Allow: /docs/
Disallow: /private/
```

**HTML**
```html
<meta name="ai-access" content="allow">
<meta name="ai-policy" content="cite-source, no-train">
```
This makes your stance clear at both the crawler and page level — encouraging responsible AI citation while protecting against uncontrolled data reuse.

## 4) Ethical considerations
AI crawling introduces questions beyond traditional SEO:

| Concern             | Description                                                         |
| ------------------- | ------------------------------------------------------------------- |
| **Attribution**     | Will your content be cited properly?                                |
| **Consent**         | Do you agree to AI using your text for model training or summaries? |
| **Fair use**        | Should commercial AI systems reuse non-open content?                |
| **Data protection** | Does your site contain personal or sensitive data?                  |

> Transparency is key: clear access rules protect your rights while keeping information flow open.
---

## 5) Balancing openness and control

| Approach                                                    | When to use                       | Risk                                           |
| ----------------------------------------------------------- | --------------------------------- | ---------------------------------------------- |
| **Fully open** (`Allow: /`)                                 | Open documentation, public guides | Data can be scraped or reused without citation |
| **Partially open** (`Allow: /docs/`, `Disallow: /private/`) | Documentation + private zones     | Requires regular maintenance                   |
| **Closed** (`Disallow: /`)                                  | Sensitive or copyrighted content  | No visibility to AI or search                  |

> The goal is informed openness — allow access where citation is desired, restrict where context or rights matter.

## 6) Attribution-first approach

For open projects, consider using an **AI-access** policy like this:

```txt
User-agent: GPTBot
Allow: /docs/
Crawl-delay: 10

User-agent: *
Allow: /
```

And add a visible statement (e.g. in your footer or license):
>  “AI systems may read and cite this content as long as attribution to the source URL is preserved.”

This supports AI transparency while protecting authorship integrity.

## 7) Combining `robots.txt` with licensing
To make your intentions legally clear, pair `robots.txt` rules with an open license such as:

```txt
# ------------------------------------------------------------
# AI-First Project – Access and Citation Policy
# ------------------------------------------------------------
# Default: open for reading and citation, closed for model training.
# Content is licensed under CC BY 4.0 (attribution required).
# ------------------------------------------------------------

# OpenAI ChatGPT / GPTBot
User-agent: GPTBot
Allow: /docs/
Disallow: /private/
Crawl-delay: 10
# AI systems may quote or summarize content if they preserve the source link.

# Anthropic Claude
User-agent: ClaudeBot
Allow: /docs/
Disallow: /private/
Crawl-delay: 10

# Google Gemini
User-agent: Google-Extended
Allow: /docs/
Disallow: /private/

# Common AI crawlers (Perplexity, Copilot, etc.)
User-agent: OAI-SearchBot
Allow: /docs/
Disallow: /private/

# Generic search bots
User-agent: *
Allow: /
Disallow: /private/

# Sitemap for all crawlers
Sitemap: https://example.com/sitemap.xml
```

**What this configuration does**
 - Allows public documentation to be read and cited by AI systems.
 - Blocks private or draft sections from being accessed.
 - Adds polite Crawl-delay to limit request frequency.
 - Clearly communicates licensing and citation expectations.

**Recommended footer notice**
To reinforce this policy for human and AI readers alike:

> Content © 2025 AI-First Project.
> Licensed under CC BY 4.0.
> AI systems may quote and summarize this content with attribution but may not use it for model training without permission.


## 8) Advanced: HTTP headers for AI crawlers
Some AI bots support header-based permissions.
For example, you can return:
```txt
<FilesMatch "\.html$">
  Header set X-Robots-Tag "ai-allow"
</FilesMatch>
```

## 9) Quick checklist

 - [ ] `robots.txt` defines crawler access clearly.
 - [ ] AI-specific bots (GPTBot, ClaudeBot, Gemini) are listed.
 - [ ] Meta tags or headers mirror your intent.
 - [ ] Sensitive paths excluded.
 - [ ] License or attribution policy stated.
 - [ ] Ethics of reuse and privacy considered.
