# CutCalc Pro v1.7.0 — Récapitulatif des modifications

**Dernière mise à jour** : 18 mai 2026  
**Fichiers modifiés** : `index.html`, `CHANGELOG.md`

---

## Ce qui a changé dans cette version

### 1. Suppression des boutons +/− des champs de saisie

Les boutons circulaires `+` et `−` qui encadraient chaque champ numérique ont été **retirés**. Ils encombraient la ligne de saisie et nuisaient à la lisibilité en conditions d'atelier. Les fonctions JS associées (`getIncStep`, `incField`) et le CSS `.inc-btn` ont également été supprimés.

Chaque ligne de saisie affiche désormais uniquement :
- L'icône badge (abréviation)
- Le libellé + symbole paramètre
- Le champ numérique
- L'unité
- Le bouton ✕ d'effacement rapide

### 2. Remplacement des pictogrammes SVG par des abréviations

Les icônes SVG dans les badges des champs de saisie (clock, speed, rpm, feed, surf, chip, power, mrr…) ont été remplacées par **l'abréviation du paramètre** correspondant (`n`, `vc`, `f`, `ap`, `D1`, `DC`, `fz`, `η`, `Pc`…).

L'abréviation est extraite automatiquement du symbole de la variable (`sym.split(/[\s\[]/)[0]`), affichée en **Open Sans Condensed Bold 13 px** couleur SPK Blue.

Avantages :
- Identification immédiate de la grandeur physique
- Meilleure lisibilité sur petit écran / avec gants
- Cohérence avec les badges de la liste de calculs

### 3. Icône d'écran d'accueil — vrai logo CutCalc (18 mai 2026)

L'icône générée par canvas (texte « SPK » + barre bleue « CERAMTEC ») a été remplacée par le vrai logo `Logo_Cutcalc.png`.

Le logo (1254×1254 px) est intégré en base64 directement dans le HTML (512×512 réduit, ~230 KB), puis redimensionné à la volée par canvas :
- **180×180** → `apple-touch-icon` (iOS Safari — ajout à l'écran d'accueil)
- **32×32** → favicon navigateur
- **192×192 + 512×512** → manifest PWA dynamique (Android / Chrome « Ajouter à l'écran »)

Un lien `<link id="app-manifest" rel="manifest">` a été ajouté dans le `<head>` ; le manifest JSON est généré en Blob URL au chargement, sans fichier externe.

---

## Fichiers à uploader sur GitHub

```
index.html        → version 1.7.0
CHANGELOG.md      → entrée v1.7.0 ajoutée
RECAP_v1.7.0.md   → ce fichier
```

## Commandes Git

```bash
cd "/c/Users/Admin/Documents/CeramTec/Cutcalc"
git add index.html CHANGELOG.md RECAP_v1.7.0.md
git commit -m "v1.7.0 — Suppression boutons +/−, abréviations en lieu des pictos"
git push
```

## Déploiement Surge

```powershell
surge "C:\Users\Admin\Documents\CeramTec\Cutcalc" cutcalc-spk.surge.sh
```

---

## Historique des versions

| Version | Date | Résumé |
|---|---|---|
| v1.7.0 | 2026-05-18 | Logo réel intégré (PWA icon iOS + Android), manifest dynamique |
| v1.7.0 | 2026-04-24 | Suppression boutons +/−, abréviations remplacent les pictos SVG |
| v1.6.0 | 2026-04-24 | Pictos techniques, ligne sélectionnée, champs ✕, bugfix layout |
| v1.5.0 | 2026-04-23 | Charte SPK CeramTec (Open Sans, couleurs officielles) |
| v1.4.1 | 2026-04-12 | Fix calc history bottom sheet |
| v1.4.0 | 2026-04-12 | Mode atelier, historique, favoris, swipe, partage |
