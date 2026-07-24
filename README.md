# MonCV.io

CV en ligne de Fabienne Saubert — site statique (HTML / CSS / JS), stylé avec Tailwind CSS v4.

## Développement

Installation des dépendances (une seule fois) :

```bash
npm install
```

Pendant que tu travailles, lance le mode surveillance : à chaque sauvegarde de
`style.css` ou d'`index.html`, le CSS est régénéré et minifié automatiquement.

```bash
npm run dev
```

Puis ouvre `index.html` dans le navigateur (`Ctrl+F5` pour forcer le rechargement du CSS).

Pour générer le CSS une seule fois, avant un commit ou un déploiement :

```bash
npm run build
```

## Organisation du CSS

| Fichier | Rôle |
| --- | --- |
| `style.css` | **Les styles perso — c'est ici qu'on écrit.** |
| `src/input.css` | Point d'entrée du build : importe Tailwind puis `style.css`. |
| `minifiedOutput.css` | **Généré — ne jamais éditer à la main.** Seul CSS chargé par `index.html`. |

⚠️ `minifiedOutput.css` doit être commité : c'est lui que le site sert en production.

## Build automatique au commit

Un hook `pre-commit` (dans `.githooks/`) régénère le CSS et l'ajoute au commit,
pour qu'un `minifiedOutput.css` périmé ne parte jamais en production. Si le build
échoue, le commit est annulé.

Il est activé automatiquement par `npm install` (script `prepare`). Pour le
configurer à la main sur un clone neuf :

```bash
git config core.hooksPath .githooks
```

Pour passer outre exceptionnellement : `git commit --no-verify`.
