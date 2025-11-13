# Forms & Interaction

AI assistants and accessibility tools need to understand **what each form or interactive element does** — not just how it looks.  
When your forms are semantically correct and labeled, both AI and humans can interact with them more reliably.

---

## 1) Clear purpose for every input

Each field must communicate its purpose through explicit HTML attributes.

```html
<label for="email">Email address</label>
<input id="email" name="email" type="email" autocomplete="email" required>
```

**Why this matters**
 - AI can identify the type of information requested (email, name, search...).
 - Browsers can autofill correctly.
 - Screen readers announce the purpose of each field.
>Always match `<label for>` with the input’s `id`.

---

## 2) Use semantic input types
Modern browsers and AI models recognize type attributes to infer meaning.
Never use `type="text"` for fields that have a more specific role.

| Type            | Meaning                  | Example                 |
| --------------- | ------------------------ | ----------------------- |
| `email`         | expects an email address | `<input type="email">`  |
| `url`           | expects a website        | `<input type="url">`    |
| `tel`           | expects a phone number   | `<input type="tel">`    |
| `number`        | numeric value            | `<input type="number">` |
| `date` / `time` | temporal input           | `<input type="date">`   |
| `search`        | search query             | `<input type="search">` |


**Benefit:**
AI assistants can prefill or simulate form submissions correctly (for example, suggesting values or understanding what a form is for).

---
## 3) Add autocomplete hints
`autocomplete` provides additional semantics for AI and browsers.

```html
<form autocomplete="on">
  <label for="fname">First name</label>
  <input id="fname" name="fname" autocomplete="given-name">

  <label for="lname">Last name</label>
  <input id="lname" name="lname" autocomplete="family-name">

  <label for="email">Email</label>
  <input id="email" name="email" type="email" autocomplete="email">
</form>
```
AI interprets `autocomplete` attributes as structured intent — for instance, that the form is about user identity rather than random text fields.

---

## 4) Use buttons with explicit intent
Use real `<button>` elements instead of clickable `<div>` or `<a>` elements for actions.
Add clear text or `aria-label` to describe what the action does.

```html
<button type="submit">Subscribe</button>
<button type="reset">Clear form</button>
<button type="button" aria-label="Open menu">☰</button>
```

> AI models and assistive tools both need textual cues to understand interactive intent.
---

## 5) Handling dynamic interaction
If a form updates dynamically (via JavaScript), make sure AI and assistive tools can detect changes.

Use `aria-live` regions to announce updates:
```html
<div aria-live="polite" id="form-status"></div>

<form onsubmit="submitForm(event)">
  <label for="email">Email</label>
  <input id="email" type="email">
  <button type="submit">Send</button>
</form>
```

```javascript
function submitForm(e) {
  e.preventDefault();
  document.getElementById("form-status").textContent = "Form submitted successfully!";
}
```
AI and screen readers can only interpret what’s reflected in the DOM.
If updates happen invisibly (e.g., with CSS-only popups), they remain unreadable.

---

## 6) Form context in JSON-LD
To help AI understand the form’s purpose, you can describe it in metadata.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "ContactForm",
  "name": "Newsletter signup",
  "description": "Form used to subscribe to AI-First Web updates.",
  "target": "https://first.ai/subscribe",
  "publisher": {
    "@type": "Organization",
    "name": "AI-First Project"
  }
}
</script>
```
> This clarifies that the form is for communication, not authentication or payment — helpful when AI summarizes your site’s functions.
---

## 7) Accessibility for interaction

Make all controls reachable and usable via keyboard only:
 - Tab order should follow logical reading order.
 - Don’t rely solely on hover effects or mouse interactions.
 - Ensure visible focus styles (:focus outline).

```css
button:focus {
  outline: 2px solid #007bff;
  outline-offset: 2px;
}
```

## 8) Validation and feedback
Avoid purely visual validation cues like red borders or icons.
Include text messages that describe the issue.
```html
<label for="email">Email address</label>
<input id="email" type="email" aria-describedby="error-email">
<span id="error-email" class="error">Please enter a valid email.</span>
```
AI reads these messages to understand how forms handle errors and user guidance.

---

## 9) Don’t hide key meaning in JavaScript
If the form relies on an AJAX request to load essential fields or messages, AI crawlers might never see them.
Instead, include essential structure and labels in the HTML itself — then enhance progressively with JS.

For AI, hidden dynamic content = invisible meaning.

---

## 10) Quick checklist
 - [ ] Each input has a `<label>` or `aria-label`.
 - [ ] Correct `type` and `autocomplete` attributes.
 - [ ] Buttons have text or accessible labels.
 - [ ] Updates announced with `aria-live` where needed.
 - [ ] Keyboard navigation works for all elements.
 - [ ] Validation includes readable text feedback.
 - [ ] No critical content loaded only via JS.
 - [ ] Optional: form purpose defined in JSON-LD.
