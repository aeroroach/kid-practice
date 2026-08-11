# AGENTS.md

## Source of truth
- `README.md` is the authoritative spec, not this file. It contains an `AI CONTEXT ANCHOR` comment block that must never be removed. Read it before any edit.
- The repo currently contains only `README.md` — `index.html` does not exist yet and must be created from scratch following the README constraints.

## Architecture constraints (from README)
- Strict single-file app: ALL HTML, CSS, and JS must live in `index.html`. No external `.css`/`.js` files, no front-end frameworks, no external fonts (Vercel compatibility, offline-capable, tablet-first).
- Quiz questions live in a cleanly commented JS array named `QUIZ_DATA` at the top of the `<script>` tag.
- "Change the topic" / "update questions" always means: rewrite only the `QUIZ_DATA` array. Do not touch CSS, animations, or scoring logic unless explicitly asked.

## UI design tokens
- Base font ≥ 18px, clean sans-serif. Touch targets ≥ 56px, spacing ≥ 16px.
- Use native Unicode emojis (no image files, no CSS-drawn shapes) in question text, options, and feedback. Graphic options: one emoji per option via `{ label, shape: { t: "emoji", e: "🌳", s: 1-3 } }`.
- Palette: soft sky-blue background, emerald green for correct, coral/pastel red for wrong, warm yellow accents. No harsh neon, no dark mode.
- Cards: centered, `border-radius: 16px`, subtle box-shadow.
- No `:hover` states (touch screen); `cursor: pointer` only for desktop preview symmetry.

## Deployment (Vercel, GitHub-linked)
- Push to `main` → auto-deploy to the primary URL (the single tablet bookmark).
- Subject branches (e.g. `feature/math`, `feature/science`) → permanent Vercel preview URLs. To ship a second topic: create a branch, swap `QUIZ_DATA`, push.
