# CutCalc Pro — Changelog

---

## v1.9.13 — 2026-06-17

### Correctif affichage — séquences `\uXXXX` littérales

- Les échappements `\uXXXX` présents dans le HTML de la bannière d'installation et du guide iOS s'affichaient tels quels (ex. `accès` au lieu de « accès », `« »` au lieu de « »).
- Converties en vrais caractères Unicode — affichage correct en FR/EN.
- Cache Service Worker bumpé en `cutcalc-v1.9.13` pour rafraîchir le cache hors-ligne.
- _S'appuie sur les versions intermédiaires v1.9.10 → v1.9.12 (UX install, auto-update du Service Worker, comparaison A/B en couleurs, unification de la version)._

---

## v1.9.8 — 2026-06-09

### PWA Installation & Wake Lock

#### Bannière d'installation native (Chrome / Edge / Android / PC)
- Événement `beforeinstallprompt` intercepté → bannière glissante depuis le bas après 5 s (une seule fois)
- Bouton **Installer** dans la bannière et dans le header (icône téléchargement)
- Clic → `prompt()` natif ; si accepté : toast de confirmation + bannière masquée
- Fermeture (✕) ou refus → flag `pwa-dismissed` en localStorage (ne réapparaît plus)

#### Guide d'installation iOS (Safari)
- Sur iPhone / iPad : sheet glissante depuis le bas expliquant les 3 étapes (Partager → Sur l'écran d'accueil → Ajouter)
- Apparaît automatiquement après 6 s si non installé et non refusé
- Bouton « Compris ! » efface définitivement le guide

#### Badge « Déjà installé »
- Si l'app tourne en mode standalone (installée), le bouton d'installation est masqué
- Événement `appinstalled` → toast + masquage du bouton

#### Wake Lock API — écran toujours allumé
- `navigator.wakeLock.request('screen')` activé à l'ouverture d'un écran de calcul (T / M / D)
- Libéré à chaque retour vers la liste, et réacquis automatiquement si l'onglet redevient visible
- Indicateur lumineux (point vert ●) affiché sur le bouton soleil dans le header

---

## v1.9.7 — 2026-06-09

### Polish UX — 5 améliorations

#### Auto-advance entre champs
- Attribut `enterkeyhint="next"` sur tous les champs numériques → le clavier mobile affiche "Suivant"
- Appui sur Enter : focus automatique sur le champ suivant visible, blur sur le dernier

#### Animation count-up sur le résultat
- Le grand chiffre s'anime de l'ancienne valeur vers la nouvelle en 160 ms (easing `ease-out-cubic` via `requestAnimationFrame`)

#### Skeleton loader sur les listes
- Les 3 listes (T / M / D) démarrent avec 4 cartes grises animées (shimmer) au chargement initial

#### Partage enrichi
- Texte restructuré : type d'opération + sous-op + tous les paramètres + formule ISO + horodatage
- Encadrement `──────────────────` pour lecture propre par SMS/e-mail

#### Comparaison A/B live
- Bouton **A/B** dans la barre d'action de chaque écran calcul (T / M / D)
- Premier tap → épingle résultat en A (bouton bleu) ; à chaque recalcul, affiche `A = x.xx u  [±δ%]` (vert/rouge/neutre)
- Second tap → efface la comparaison ; Reset ↺ efface le pin automatiquement

---

## v1.9.0 — 2026-06-03

### Refonte UI — lisibilité & ergonomie atelier

- **Header désencombré** : les toggles FR/EN et mm/inch sont déplacés dans un nouveau **panneau Réglages** (icône engrenage) qui glisse du bas. Le header ne garde que logo + Réglages + Historique + Mode sombre.
- **Pictogrammes T/M/D redessinés** (barre de navigation) en vues de profil reconnaissables : tournage (pièce horizontale + outil), fraisage (fraise à bout plat), perçage (foret pointu dans un bloc).
- **Pictogrammes sous-opérations** (EXT/FACE/GORGE/TRONÇ.) redessinés et **labels texte ajoutés** ; état actif avec fond bleu plein. GORGE vs TRONÇONNAGE nettement différenciés (rainure au milieu vs pièce qui se détache).
- **Zone résultat** : valeur agrandie 52→76 px, formule 9→13 px, unité 13→18 px, badge grandeur en pastille, boutons d'action 28→44 px (cibles tactiles atelier).
- **Champs de saisie aérés** : lignes 52→60 px, badges 34→38 px, champ de saisie 38→44 px / 20 px.
- **Cartes de liste** : formule 10→11 px, chevron plus visible.
- **Mode sombre** vérifié sur l'ensemble de la refonte.

### Corrections

- Formule périmée dans le guide intégré : `hm = f × √(ap/IC)` → `hm = f × sin(Kr)` (cohérent avec le moteur v1.8.4).
- Versions périmées (guide + à-propos) harmonisées en v1.9.0.
- Service Worker : cache `cutcalc-v1.9.0`.

---

## v1.8.4 — 2026-05-28

### Correction T_hm — Épaisseur copeau tournage plaquette ronde

- **Formule corrigée** (tournage, mode plaquette ronde) :
  - ❌ Ancienne : `hm = fr × √(ap/IC)` — sous-estimait le résultat (~45%)
  - ✅ SPK officielle : `Kr = arccos(1 − ap/R)` puis `hm = fr × sin(Kr)` avec `R = IC/2`
  - Exemple RNGN 12 (IC=12,70 mm, R=6,35 mm), ap=2 mm, fr=0,15 mm :
    - Avant : **0,060 mm** ✗ → Après : **0,109 mm** ✓
- La formule affichée sous le résultat se met à jour dynamiquement en mode plaquette ronde

---

## v1.8.3 — 2026-05-27

### Fonctionnement 100% hors-ligne (offline)

- **Polices embarquées en base64** : Open Sans (300/400/600/700), Open Sans Condensed (700) et DM Mono (400/500) sont désormais intégrées directement dans le HTML en tant que `@font-face` data URI (woff2 latin, ~312 KB base64) — aucune requête externe n'est nécessaire
- **Suppression de la dépendance Google Fonts** : le `<link>` vers `fonts.googleapis.com` a été retiré ; `fonts.gstatic.com` n'est plus jamais appelé
- **Service Worker mis à jour** : cache `cutcalc-v1.8.3`, Google Fonts retiré du tableau `ASSETS` — l'app démarre et s'affiche correctement sans réseau après la première visite
- L'application est désormais entièrement autonome : HTML + CSS + JS + polices dans un seul fichier

---

## v1.8.2 — 2026-05-27

### Épaisseur copeau fraisage — auto-sélection de formule

- **M_hex1 + M_hex3 fusionnés** en une seule entrée **"Épaisseur copeau fraise"** (`M_hex`)
- L'app détecte automatiquement le régime selon `ae` vs `DC/2` :
  - `ae ≤ DC/2` → `hex = 2×fz×sin(κ)×√(ae/DC−(ae/DC)²)`
  - `ae > DC/2` → `hex = fz×sin(κ)`
- La formule affichée sous le résultat se met à jour en temps réel selon le régime détecté
- **M_hex2** (plaquette ronde) conservé séparément — inputs différents (`ap`, `IC`)

### Suppression du mode atelier

- Bouton ☀, CSS `.workshop-mode`, variable `WORKSHOP` et fonction `toggleWorkshop()` supprimés
- Entrée retirée du guide utilisateur

---

## v1.8.1 — 2026-05-27

### Correction de formules — fraisage (source : catalogue officiel SPK CeramTec)

- **M_hex1 — Épaisseur copeau (ae ≤ DC/2)** : formule corrigée
  - ❌ Ancienne : `hex1 = fz × sin(κ) × √(ae/DC)`
  - ✅ Officielle : `hex1 = 2 × fz × sin(κ) × √(ae/DC − (ae/DC)²)`
  - Impact : résultat sous-estimé d'un facteur ~1.7 en engagement typique (ae = DC/4)

- **M_hex2 — Épaisseur copeau plaquette ronde** : formule corrigée
  - ❌ Ancienne : `hex2 = fz × √(ap/IC)`
  - ✅ Officielle : `hex2 = 2 × fz × √(ap/IC − (ap/IC)²)`
  - Impact : résultat sous-estimé d'un facteur ~1.7 en engagement typique (ap = IC/4)

- **T_H et M_H — Puissance en chevaux** : facteur de conversion corrigé
  - ❌ Ancien : `H = Pc × 1.341` (HP mécaniques US)
  - ✅ Officiel SPK : `H = Pc / 0.75` (convention catalogue CeramTec)

- Strings de formule dans le guide mis à jour en cohérence

---

## v1.8.0 — 2026-05-18

### 5 upgrades majeurs

- **Matériaux persistants** : la sélection Kc (force spécifique) et HB (dureté) est mémorisée via `localStorage` et restaurée automatiquement à chaque calcul — plus besoin de re-sélectionner sa matière à chaque fois
- **Unités mm/inch** : le toggle existant effectue désormais une vraie conversion (×÷25.4) de tous les champs de saisie en temps réel ; les labels se mettent à jour instantanément
- **Export PDF** : nouveau bouton 🖨 dans la barre de résultat (T / M / D) — génère une fiche de calcul formatée (titre, formule, paramètres, résultat, notes, date) imprimable / exportable en PDF via Safari ou Chrome
- **Préférences persistantes** : langue, dark mode et unité sont sauvegardés dans `localStorage` et restaurés au démarrage — l'app retrouve son état au prochain lancement
- **Haptic feedback & erreurs lisibles** : vibration 30 ms (`navigator.vibrate`) sur chaque résultat calculé ; affichage `—` rouge en lieu et place de `0` lorsque les entrées sont invalides ou manquantes

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
