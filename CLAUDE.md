# Quiz HTML Template – CLAUDE.md

This file describes the format and design spec for the "Test Your Knowledge" interactive quiz pages used in *Materials Evaluation* (ME-ASNT). Use this as a reference when generating new quiz HTML files.

---

## Overview

Each quiz is a **single self-contained HTML file** with no external dependencies. It displays one question at a time on a stacked card, with clickable answer options that reveal correct/incorrect feedback immediately on selection.

---

## File Naming Convention

```
test-your-knowledge-[topic].html
```

Example: `test-your-knowledge-leak-testing.html`

---

## Design Spec

### Color Palette

| Element | Value |
|---|---|
| Page background | `#f0f4f8` |
| Cover card / question card background | `linear-gradient(135deg, #1a2e4a 0%, #2d5282 100%)` |
| Cover card accent | `linear-gradient(135deg, #1a2e4a 0%, #2b4c7e 100%)` |
| Accent / label blue | `#90cdf4` |
| Body text on dark | `#e2e8f0` |
| Correct answer highlight | `rgba(39,103,73,0.55)` border `#68d391` |
| Wrong answer highlight | `rgba(155,44,44,0.35)` border `#fc8181` |
| Score card background | `linear-gradient(135deg, #276749 0%, #38a169 100%)` |
| Footer text | `#718096` |

### Typography

- Font family: `'Segoe UI', Arial, sans-serif`
- Page title (`h1`): `2rem`, uppercase, letter-spacing `2px`, color `#1a2e4a`
- Subtitle: `0.95rem`, color `#4a5568`
- Question number label: `0.72rem`, uppercase, letter-spacing `2px`, color `#90cdf4`
- Question text: `1.05rem`, font-weight `600`, color `#fff`
- Answer option text: `0.92rem`, color `#e2e8f0`
- Answer letter: font-weight `700`, color `#90cdf4`

### Layout

- Max content width: `640px`, centered
- Cover banner + question card stacked vertically with `gap: 20px`
- Card border-radius: `14px`
- Card box-shadow: `0 4px 18px rgba(0,0,0,0.12)`
- Page padding: `40px 20px`

---

## Quiz Behavior

1. **One question at a time** — only the current question card is shown.
2. **Selectable answers** — each option is a `<button>` inside a `<ul>`. Clicking locks in the answer.
3. **Immediate feedback** — on click:
   - Correct option turns green (`.correct` class)
   - Selected wrong option turns red (`.wrong` class)
   - A result badge appears above the options: green "✓ Correct!" or red "✗ Incorrect – correct answer: [x]. [answer text]"
   - All buttons are disabled after answering
4. **Navigation** — PREV / NEXT buttons at the bottom of the card.
   - NEXT is disabled until the current question is answered.
   - On the last question, NEXT becomes "FINISH ✓" once answered.
5. **Progress dots** — row of dots between nav buttons. ○ = unanswered, ● = correct, ◉ = incorrect.
6. **Score card** — shown after finishing all questions. Displays score as `X / N` with a contextual message and a "Try Again" button.

### Score Messages

| Score % | Message |
|---|---|
| 100% | "Perfect score! Outstanding work." |
| 80–99% | "Great job! Strong understanding of [topic]." |
| 60–79% | "Good effort. Review the missed questions and try again." |
| < 60% | "Keep studying – you'll get there!" |

---

## Data Structure

Questions are defined as a JavaScript array of objects:

```js
const questions = [
  {
    q: "Question text here?",
    options: ["Option A", "Option B", "Option C", "Option D"],
    correct: 0  // zero-based index of the correct answer
  },
  // ... more questions
];
```

- Always 4 answer options (a, b, c, d)
- `correct` is the **zero-based index** of the correct answer

---

## Footer

```html
<footer>
  Source: <em>[Publication Title]</em>, [edition] &nbsp;|&nbsp; Materials Evaluation, [Month Year]
</footer>
```

Example:
```
Source: ASNT Level III Study Guide: Leak Testing, second edition | Materials Evaluation, March 2026
```

---

## How to Generate a New Quiz

When asked to create a new quiz in this format, provide:

1. **Topic name** (e.g., "Radiographic Testing")
2. **Cover card description** — one or two sentences describing the quiz and its source
3. **Questions** — 3–10 questions, each with 4 options and one correct answer
4. **Footer source line** — publication title, edition, and issue date

Claude will produce a complete, self-contained HTML file following all specs above. The file should require no external scripts, fonts, or stylesheets.

---

## Example Prompt

> Create a "Test Your Knowledge" quiz HTML file on **Radiographic Testing** with 5 questions from the *ASNT Level III Study Guide: Radiographic Testing*, third edition. Issue: Materials Evaluation, April 2026.
