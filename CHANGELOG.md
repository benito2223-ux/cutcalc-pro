# CutCalc Pro — Changelog

---

## v1.7.1 — 2026-05-18

### Icône écran d'accueil — vrai logo (iOS + Android)

- **Remplacement de l'icône canvas** : la génération programmatique (texte « SPK » + barre bleue « CERAMTEC ») est remplacée par le vrai `Logo_Cutcalc.png` intégré en base64 (512×512 px, ~230 KB)
- **Apple Touch Icon** : 180×180 px via canvas — affiché lors de l'ajout à l'écran d'accueil sur iOS Safari
- **Favicon** : 32×32 px
- **Manifest PWA dynamique** : généré en Blob URL au chargement, fournit les icônes 192×192 et 512×512 pour l'installation Android/Chrome (« Ajouter à l'écran d'accueil »)
- Ajout de `<link id="app-manifest" rel="manifest">` dans le `<head>`

---

## v1.7.0 — 2026-04-24

### Guide utilisateur bilingue intégré

- **Panneau d'aide glissant** : accessible via le bouton ℹ dans la barre de navigation, s'ouvre en overlay depuis la droite
- **Contenu bilingue FR/EN** : 8 sections (navigation, calculs, historique, partage, favoris, unités, mode atelier, à propos) — toutes les chaînes basculent avec le toggle langue existant
- **Logo SPK** dans l'en-tête du guide
- **Design cohérent** avec la charte SPK CeramTec (couleurs, typographie Open Sans)

### Suppression des boutons +/− et remplacement des pictos SVG

- **Boutons +/−** supprimés de chaque champ de saisie (encombrement, mauvaise lisibilité atelier) — fonctions JS `getIncStep` / `incField` et CSS `.inc-btn` retirés
- **Pictos SVG** (clock, speed, rpm, feed…) remplacés par l'**abréviation du paramètre** (`vc`, `n`, `f`, `ap`, `DC`…) en Open Sans Condensed Bold 13 px couleur SPK Blue
- Chaque ligne de saisie affiche : badge abréviation · libellé · champ · unité · bouton ✕

### Icône écran d'accueil — canvas auto-généré *(remplacé en v1.7.1)*

- Génération d'une icône 180×180 px par canvas (fond sombre, texte SPK, barre CERAMTEC)
- Favicon 32×32 synchronisé

---

## v1.6.0 — 2026-04-24

### UX & Interface

- **Pictogrammes techniques** dans les badges des champs de saisie (clock, speed, rpm, feed, surf, chip, power, mrr…) via icônes SVG inline
- **Ligne de calcul sélectionnée** mise en évidence (fond bleu pâle + bordure SPK blue)
- **Bouton ✕ d'effacement rapide** sur chaque champ numérique
- **Bugfix layout** : correction de débordements et espacements sur petits écrans

---

## v1.5.0 — 2026-04-23

### Brand Update — SPK by CeramTec Design System

Mise à jour complète de la charte graphique pour aligner l'application sur le **Design System officiel SPK by CeramTec**.

#### Typographie
- **Police principale** : `Barlow` → `Open Sans` (300 / 400 / 600 / 700)
- **Police condensée** : `Barlow Condensed` → `Open Sans Condensed` (700) — titres, valeurs résultat, symboles d'opérations
- **Police monospace** : `DM Mono` conservée pour les formules et valeurs techniques
- Harmonisation des `font-weight` : graisses 800 ramenées à 700 (limite Open Sans Condensed)

#### Couleurs
| Token | Avant | Après |
|---|---|---|
| `--spk-blue` | `#1565C0` | `#1B5EA6` |
| `--spk-blue-d` | `#0D47A1` | `#154d8a` |
| `--spk-blue-l` | `#1976D2` | `#2E6FAD` |
| `--spk-blue-pale` | `rgba(21,101,192,.08)` | `rgba(27,94,166,.08)` |
| `--ct-red` | `#E3000F` | `#E2001A` |
| `--ct-red-pale` | `rgba(227,0,15,.08)` | `rgba(226,0,26,.07)` |
| `--ct-red-glow` | `rgba(227,0,15,.18)` | `rgba(226,0,26,.18)` |

- Mise à jour de toutes les couleurs hardcodées dans les icônes SVG inline

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
