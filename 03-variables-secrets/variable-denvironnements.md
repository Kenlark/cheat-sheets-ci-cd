# Utilisation des variables d'environnement GitHub Actions

## Exemple lors d'un déploiement sur un VPS

- `NODE_ENV`: Indique l'environnement d'exécution de l'application (par exemple, `production`).
- `DATABASE_URL`: L'URL de connexion à la base de données de votre application.
- `VPS_HOST`: L'adresse IP ou le nom de domaine de votre VPS.
- `VPS_USERNAME`: Le nom d'utilisateur pour la connexion SSH à votre VPS.

```yaml
name: Deploy Web Application

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    env:
      NODE_ENV: production
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: "14"

      - name: Install dependencies
        run: npm install

      - name: Build
        run: npm run build
        env:
          DATABASE_URL: ${{ secrets.DATABASE_URL }}

      - name: Deploy to VPS
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.VPS_HOST }}
          username: ${{ secrets.VPS_USERNAME }}
          key: ${{ secrets.SSH_PRIVATE_KEY }}
          script: |
            cd /path/to/your/app
            git pull
            npm install --production
            pm2 restart all
```

### Explication

- **Variables d'Environnement au Niveau Job** : `NODE_ENV` est définie pour tout le job, indiquant que l'application doit s'exécuter en mode production.
- **Variables d'Environnement au Niveau Étape** : `DATABASE_URL` est utilisée uniquement lors de la construction de l'application, garantissant que l'accès à la base de données est sécurisé.
- **Utilisation des Secrets** : `VPS_HOST`, `VPS_USERNAME`, et `SSH_PRIVATE_KEY` sont stockés comme secrets et utilisés pour établir une connexion sécurisée au VPS pour le déploiement.

## Résumé

Les variables d'environnement constituent un pilier dans la configuration des workflows CI/CD sur GitHub Actions, offrant une méthode sécurisée et flexible pour gérer des informations de configuration spécifiques aux environnements de développement, de test, et de production.

- **Stockage et Application** : Vous avez appris que les variables d'environnement peuvent être configurées à différents niveaux, y compris directement dans les fichiers de workflow YAML, au niveau des secrets de dépôt pour une utilisation transversale, ou même au niveau de l'organisation pour un partage entre plusieurs dépôts.

- **Exemple d'Utilisation** : À travers un scénario pratique, vous avez vu comment déployer une application web Node.js sur un VPS en utilisant des variables d'environnement pour gérer des aspects critiques tels que les configurations de l'environnement d'exécution, la connexion à la base de données, et les détails de la connexion SSH au VPS.

- **Bonnes Pratiques** : Enfin, ce module a souligné l'importance de sécuriser les variables d'environnement, en particulier celles contenant des données sensibles, en les déclarant comme secrets et en limitant leur portée d'utilisation aux étapes spécifiques du workflow où elles sont nécessaires.
