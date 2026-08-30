# Kid's Practice Quiz Engine

<!-- AI CONTEXT ANCHOR: DO NOT REMOVE -->
<!-- PURPOSE: Single-page interactive quiz application optimized for tablet touchscreens -->
<!-- ARCHITECTURE: Strict single-file architecture. All HTML, CSS, and JS must reside in index.html -->
<!-- VISUAL THEME: Kid-friendly, high-contrast, rounded UI, no tiny touch targets -->
<!-- DEPLOYMENT: Vercel automated pipeline linked via GitHub branches -->

This repository serves as a flexible, AI-managed quiz application built for a child's educational practice on a tablet.

---

## 🛠 Application Architecture & Constraints

To ensure maximum compatibility with Vercel and effortless file transfers, the entire application **must follow these rules**:

1. **Single File Only**: Everything must live inside `index.html`. Do not generate external `.css` or `.js` files.
2. **Offline Capable**: Avoid external dependencies (like heavy front-end frameworks or external fonts). Use native Web APIs and standard semantic HTML5.
3. **Data Isolation**: The quiz questions must be stored in a clean, clearly commented JavaScript array named `QUIZ_DATA` at the top of the `<script>` tag. Options may be plain strings or `{ label, shape: { t: "emoji", e: "🌳", s: 1-3 } }` objects for emoji graphics. This allows easy topical rewrites without touching the UI rendering logic.
4. **Practice Sets & Question Pool**: `QUIZ_DATA` is a *pool* of questions, each tagged with a `set` id (spelling, grammar, dialog, polite, reading, etc.). A `QUIZ_SETUP` object next to it defines the set order and how many questions each set samples. Each run (fresh load or "Try Again") randomly samples and shuffles the pool, so **retries always present different questions**. The 🔊 Listen button (native SpeechSynthesis, offline) appears **only on questions carrying a `listen` field** — typically spelling words — so it never reads blanks (___), nor reveals answers on dialog questions. The `reading` set uses `type: "find"` questions (`para` + `foods`): the whole paragraph is shown and every word is a tappable chip; tapping a food word turns it green, tapping any other word counts a mistake (red flash). The round completes when all food words are found; scored correct if mistakes ≤ 2.

---

## 🎨 UI Style & Design System Guidelines

When styling or modifying the interface, adhere to the following **Generic Kid-Friendly Theme**:

* **Color Palette**: Bright, inviting, and high-contrast colors (e.g., Soft Sky Blue backgrounds, Emerald Green for success states, Coral/Pastel Red for errors, and Warm Yellow accents). Avoid harsh neon or sterile corporate dark modes.
* **Typography**: Large, clean, highly legible sans-serif fonts (minimum base size of `18px`).
* **Emoji Graphics**: Use native Unicode emojis (never image files or CSS-drawn shapes) for question text, answer options, and feedback. Emojis render offline on any device with zero dependencies and keep the quiz visually engaging for young kids. For graphic answer choices, pair one emoji per option with a short text label.
* **Touch Targets**: All interactive elements (buttons, answer choices) must have a minimum height/width of `56px` with generous spacing (`16px+`) to prevent accidental misclicks on a tablet touchscreen.
* **Component Layout**:
  * **Header**: Large title indicating the current topic and a visible progress bar (e.g., "Question 3 of 10").
  * **Card Area**: Centered container with smooth rounded corners (`border-radius: 16px;`) and subtle box-shadows.
  * **Feedback**: Instant, highly visual, non-punitive feedback when an answer is tapped (green for correct, red/orange for incorrect).
  * **Score Screen**: A celebration layout summarizing the final score with a large "Try Again" or "Reset" button.

---

## 🚀 Branching & Deployment Strategy

This repository uses Vercel for continuous deployment. It supports two distinct content delivery workflows:

### Workflow A: The Continuous Overwrite (Default)
Modifications are made directly to the `main` branch. 
* **Action**: Rewrite the `QUIZ_DATA` array inside `index.html` on `main`.
* **Result**: Vercel instantly updates the primary URL (e.g., `kids-quiz.vercel.app`), maintaining a single bookmark on the tablet.

### Workflow B: Subject-Specific Branches (Multi-Topic)
New topics are created on isolated Git branches named after the subject (e.g., `feature/math`, `feature/science`).
* **Action**: Create a new branch, swap the `QUIZ_DATA` array, and push to GitHub.
* **Result**: Vercel generates a unique, permanent Preview URL for that branch. This allows multiple active quizzes to exist simultaneously via different tablet bookmarks.

---

## 🤖 Instructions for AI Coding Agents (OpenCode)

When initialization (`/init`) occurs or updates are requested:
1. **Always read this README first** to align with the single-file architectural constraint and design tokens.
2. When asked to "change the topic" or "update questions," **only rewrite the contents of `QUIZ_DATA`** (and, if needed, the set names/counts in `QUIZ_SETUP`). Do not alter the underlying CSS structure, animations, or scoring logic unless explicitly instructed. Keep each set's pool larger than its sampled count so retries vary.
3. Ensure all generated interactive elements lack `hover` states (as they do not apply to touch screens) and utilize `cursor: pointer` primarily for desktop previewing symmetry.
4. **Question quality — no straight-forward recall.** Do not write questions where the answer just repeats the cue (e.g., "Meat goes in the freezer → which method?" answered by echoing "freezing"). Prefer short scenario-based questions that require a reasoning step: a mini-story with distractors (e.g., ice cream left out on a hot day, milk that must stay cool but not frozen), "why does this method work?" questions, or "which food uses this method?" reversed matchings. Build all content only from the topic's source material and keep it at the child's grade level.
# kid-practice
