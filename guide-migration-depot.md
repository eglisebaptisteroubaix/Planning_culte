# Migration du dépôt GitHub — guide pas à pas

Ce guide explique comment passer de `Planning_culte_2026` à un dépôt permanent `Planning_culte`,
valable pour toutes les années futures sans changer l'URL.

---

## Pourquoi faire cette migration ?

Actuellement, l'URL de l'appli est :
`https://eglisebaptisteroubaix.github.io/Planning_culte_2026/`

Si vous créez un nouveau dépôt chaque année, l'URL change et il faut re-communiquer
le lien à 70 intervenants. En renommant le dépôt une seule fois, l'URL devient :
`https://eglisebaptisteroubaix.github.io/Planning_culte/`

Ce lien ne changera plus jamais. Vous déposez simplement un nouveau `index.html`
chaque année sur ce même dépôt.

---

## Étape 1 — Renommer le dépôt sur GitHub

1. Allez sur **https://github.com/eglisebaptisteroubaix/Planning_culte_2026**
2. Cliquez sur **Settings** (onglet en haut à droite du dépôt)
3. Tout en haut de la page Settings, vous voyez **Repository name**
4. Effacez `Planning_culte_2026` et tapez `Planning_culte`
5. Cliquez sur **Rename**

GitHub affiche un avertissement : *"This will break existing links."*
C'est normal — GitHub redirige automatiquement l'ancienne URL vers la nouvelle
pendant une période transitoire. Confirmez.

---

## Étape 2 — Vérifier que GitHub Pages est bien activé

1. Toujours dans **Settings**, cliquez sur **Pages** dans le menu de gauche
2. Vérifiez que la source est bien **Deploy from a branch → main → / (root)**
3. L'URL affichée doit maintenant être :
   `https://eglisebaptisteroubaix.github.io/Planning_culte/`

Si l'URL n'a pas encore changé, attendez 1 à 2 minutes et rafraîchissez la page.

---

## Étape 3 — Déposer les fichiers mis à jour

Déposez les deux fichiers sur le dépôt renommé :

- **`index.html`** — Planning des cultes 2026 (version mise à jour avec code DIMANCHE91)
- **`calendrier-staff.html`** — Calendrier Staff (valable jusqu'en 2035, aucune mise à jour annuelle)

Pour déposer un fichier sur GitHub sans ligne de commande :
1. Allez sur la page principale du dépôt `Planning_culte`
2. Cliquez sur le fichier à remplacer (ex. `index.html`)
3. Cliquez sur l'icône crayon ✏ (Edit this file) en haut à droite
4. En bas de la page, cliquez **"Upload file"** ou collez le nouveau contenu
5. Cliquez **Commit changes**

Ou plus simplement : cliquez **Add file → Upload files**, glissez les deux fichiers,
puis **Commit changes**.

---

## Étape 4 — Communiquer les nouvelles URLs au Staff et aux intervenants

**URL Planning des cultes (intervenants) :**
`https://eglisebaptisteroubaix.github.io/Planning_culte/`

**URL Calendrier Staff :**
`https://eglisebaptisteroubaix.github.io/Planning_culte/calendrier-staff.html`

**Codes d'accès :**
- Calendrier Staff : `Staff91`
- Administrateur (les deux applis) : `DIMANCHE91`

---

## Ce que vous ferez chaque année (janvier)

### Pour le Planning des cultes

1. Préparez le nouveau `index.html` pour l'année suivante
   (nouveaux dimanches, nouveaux prédicateurs, etc.)
2. Déposez-le sur le dépôt `Planning_culte` en remplacement de l'ancien
3. L'URL reste identique — aucune communication à refaire

### Pour le Calendrier Staff

**Rien à faire.** Le calendrier génère automatiquement les semaines
de 2026 à 2035. Les événements de département sont stockés dans Firebase
et restent accessibles quelle que soit l'année.

La seule mise à jour utile (mais facultative) : si vous voulez que les
infos culte (prédicateur, type de culte) apparaissent automatiquement
dans le Calendrier Staff pour la nouvelle année, il faut créer dans Firebase
la collection `planning_culte_2027` avec un document `overrides`. Cela se fait
automatiquement dès que quelqu'un saisit la première inscription dans
l'appli Planning des cultes 2027.

---

## Récapitulatif des collections Firebase

| Collection | Usage | Mis à jour par |
|---|---|---|
| `planning_culte_2026` | Inscriptions culte 2026 | Appli Planning des cultes |
| `planning_culte_2027` | Inscriptions culte 2027 | Appli Planning des cultes (dès 2027) |
| `calendrier_staff` | Tous les événements Staff | Appli Calendrier Staff |

Les deux applis lisent `planning_culte_YYYY` en lecture (Calendrier Staff)
et en écriture (Planning des cultes). Firebase gère les droits via les règles
Firestore déjà en place.
