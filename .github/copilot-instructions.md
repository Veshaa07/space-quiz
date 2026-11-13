# Copilot instructions

## Build, test, and lint

- The project is a standalone HTML page and has no configured build, test, lint, or package-manager commands.
- To run it, open `space-quiz.html` directly in a browser; it does not need a server.
- For a focused manual check, answer one question and verify the feedback, score, and progress before continuing. For a full smoke test, complete all ten questions, verify the results, and restart.

## Architecture

- `space-quiz.html` contains the entire application: semantic page markup, responsive CSS, theme definitions, quiz data, and interaction logic. Keep it self-contained unless the project is deliberately expanded.
- The quiz state (`current`, `score`, and `answered`) is managed in the inline script. `renderQuestion()` builds the answer buttons from the `questions` array; `chooseAnswer()` handles feedback, scoring, and progress; `nextQuestion()` advances to `showResults()`; the restart handler resets state and renders the first question.
- Visual tokens live in CSS custom properties on `:root`, with dark-theme overrides on `:root[data-theme="dark"]`. The theme toggle sets that attribute. Keep new colors in these tokens so both themes stay consistent.
- The page uses a centered, narrow card layout. Responsive adjustments and reduced-motion behavior are in the page stylesheet.

## Codebase conventions

- Add quiz content as entries in the `questions` array. Each entry has a `category`, `emoji`, `question`, four `answers`, a zero-based `correct` answer index, and a short `fact`. Keep the correct index aligned with the answer order.
- Keep answer text and explanatory facts as plain text, assigning user-visible strings with `textContent`. Answer buttons are generated as native `<button>` elements; preserve keyboard operation and the existing focus styling.
- Keep dynamic progress synchronized across its visible label, fill width, and `aria-valuenow`. Feedback uses the existing live status region, and decorative emoji or labels should remain hidden from assistive technology where marked `aria-hidden`.
- Maintain both theme variants and the `prefers-reduced-motion` override when changing visual effects or animations.
