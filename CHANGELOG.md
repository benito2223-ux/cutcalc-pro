# CutCalc Pro — Changelog

---

## v1.4.1 — 2026-04-12

### Bug Fixes
- **Calc history bottom sheet** — Added all missing CSS (`.history-sheet`, `.history-overlay`, `.history-sheet-handle`, `.history-sheet-header`, `.history-sheet-title`, `.history-sheet-close`, `.history-sheet-list` + `.show` transition states). The sheet was completely invisible before this fix.
- **HTML structure** — Moved `history-overlay` and `history-sheet` outside the `hist-panel` div. They were nested inside a `position:fixed` + `transform: translateX(100%)` ancestor, which caused `position:fixed` children to be clipped to that ancestor's stacking context and permanently off-screen.

---

## v1.4.0 — 2026-04-12

### New Features
1. **Result font size 60px minimum** — `.res-val` set to 60px; workshop mode bumps it to 72px.
2. **Workshop mode** — Ultra high contrast toggle (sun icon, top-right header). Black background, enlarged fonts, orange accent on active state.
3. **Quick +/− increment buttons** — Every numeric input field has `−` and `+` buttons with smart step values per field type (e.g. 0.05 for feed, 1 for diameter, 100 for RPM).
4. **Calculation history** — Bottom sheet showing last 5 calculations per operation (in-session). Tap the clock icon in the result area to open. Tap any entry to restore those input values.
5. **Favorites star system** — Star any calculation from the list screen. Starred items float to the top, persisted via `localStorage`.
6. **Swipe navigation** — Swipe left/right between turning sub-operations (Ext → Face → Groove → Cutoff) with animated dot indicators.
7. **Result sharing** — Share button uses Web Share API with clipboard fallback. Shares result, inputs, and note as formatted text.
8. **Calculation notes** — Expandable textarea below inputs for part name, material, or operation notes. Included in share output.
9. **Mobile input attributes** — All numeric inputs have `inputmode="decimal"` and `pattern="[0-9]*"` for correct mobile keyboard.
10. **UX polish** — Top accent bar (3px SPK blue), CSS transitions on all interactive elements, `min-height: 52px` touch targets on input rows.

### Infrastructure
- Git repository initialized at `C:\Users\Admin\Documents\SPK Tools\SPK Cut Calc`
- Published to GitHub: https://github.com/benito2223-ux/cutcalc-pro
- Deployed to surge: https://cutcalc-spk.surge.sh
