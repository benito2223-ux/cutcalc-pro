# CutCalc Pro — SPK by CeramTec

**v1.5.0** · Application web mobile de calcul d'usinages, aux couleurs du Design System SPK by CeramTec.

---

## Présentation

CutCalc Pro est une PWA monopage (fichier `index.html` unique) conçue pour les techniciens et opérateurs qui utilisent des outils de coupe SPK by CeramTec. Elle permet de calculer rapidement les paramètres d'usinage : vitesse de coupe, avance, profondeur de passe, RPM, etc.

L'application fonctionne entièrement hors-ligne une fois chargée, sans dépendance à un serveur backend.

---

## Fonctionnalités principales

- **Calculateurs multi-opérations** — Tournage (ext., dressage, gorge, tronçonnage), fraisage, perçage et plus
- **Résultat toujours visible** — Zone de résultat fixe en haut de l'écran pendant la saisie
- **Mode atelier** — Contraste ultra-élevé, police agrandie pour utilisation en conditions lumineuses difficiles
- **Historique de calculs** — 5 derniers résultats par opération, rappelables d'un tap
- **Navigation par swipe** — Glisser gauche/droite entre les sous-opérations de tournage
- **Partage de résultats** — Web Share API avec fallback presse-papier
- **Favoris** — Épingler les opérations fréquentes (persisté en localStorage)
- **Notes de calcul** — Zone de texte libre associée à chaque calcul (référence pièce, matière, etc.)
- **Bilingue FR / EN** — Bascule de langue intégrée

---

## Charte graphique

L'application respecte le **Design System SPK by CeramTec** :

| Élément | Valeur |
|---|---|
| Couleur principale | `#1B5EA6` (SPK Blue) |
| Couleur accent | `#E2001A` (CeramTec Red) |
| Police corps | Open Sans 400 / 600 / 700 |
| Police titres | Open Sans Condensed 700 |
| Police technique | DM Mono 400 / 500 |
| Border-radius | 3px (cartes) · 7–11px (inputs) |

---

## Structure du projet

```
cutcalc-pro/
├── index.html      # Application complète (HTML + CSS + JS inline)
├── README.md       # Ce fichier
└── CHANGELOG.md    # Historique des versions
```

Tout le code est contenu dans `index.html`. Il n'y a pas de build step, pas de bundler, pas de dépendances npm.

---

## Déploiement

### GitHub Pages

1. Aller dans **Settings → Pages** du repo
2. Source : `Deploy from a branch` → branche `main` → dossier `/` (root)
3. L'URL sera : `https://<username>.github.io/cutcalc-pro/`

### Surge.sh

```bash
npm install -g surge
surge . cutcalc-spk.surge.sh
```

### Déploiement manuel

Copier `index.html` sur n'importe quel hébergement statique (Netlify Drop, Vercel, etc.). Aucune configuration serveur requise.

---

## Mise à jour du repo

```bash
git add index.html CHANGELOG.md README.md
git commit -m "v1.5.0 — Mise à jour charte graphique SPK CeramTec"
git push origin main
```

---

## Licence

Usage interne SPK by CeramTec. Non destiné à une distribution publique.
