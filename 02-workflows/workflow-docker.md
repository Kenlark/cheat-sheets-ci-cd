# Intégration avec Docker

## 6.3.1 Configuration d'un Workflow Docker avec GitHub Actions

L'utilisation de Docker dans un workflow GitHub Actions se fait généralement en deux phases : la construction de l'image Docker et son déploiement.

### Construction de l'Image Docker

1. **Définir un Dockerfile** : Commencez par créer un Dockerfile dans votre projet, décrivant l'environnement d'exécution de votre application.

2. **Construire l'Image dans GitHub Actions** :
   - Utilisez une étape dans votre workflow pour construire l'image Docker à partir de votre Dockerfile, en utilisant la commande `docker build`.

### Déploiement de l'Image Docker

1. **Push de l'Image sur un Registry** : Après la construction, poussez l'image sur Docker Hub ou un autre registry Docker, en utilisant `docker push`.

2. **Déploiement sur le Serveur** :
   - Configurez votre serveur pour tirer et exécuter l'image Docker mise à jour, en utilisant des secrets GitHub pour stocker de manière sécurisée les informations d'authentification du registry.

## 6.3.2 Exemple de Workflow

```yaml
name: CI/CD avec Docker

on:
  push:
    branches:
      - main

jobs:
  build-and-push:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Build Docker image
        run: docker build . -t monapp:latest

      - name: Push to Docker Hub
        run: |
          echo ${{ secrets.DOCKER_PASSWORD }} | docker login -u ${{ secrets.DOCKER_USERNAME }} --password-stdin
          docker push monapp:latest
```

La commande de run effectue deux opérations principales :

1. **Login au Docker Hub** : Utilise `echo` pour passer le mot de passe Docker au client Docker via `stdin`, en utilisant l'option `--password-stdin`. Cela permet une connexion sécurisée sans avoir besoin d'écrire le mot de passe en clair dans le script. Les valeurs `${{ secrets.DOCKER_USERNAME }}` et `${{ secrets.DOCKER_PASSWORD }}` sont des variables d'environnement qui doivent être définies dans les secrets de votre dépôt GitHub. Elles contiennent respectivement votre nom d'utilisateur et votre mot de passe pour Docker Hub.

2. **Push de l'Image Docker** : Après une connexion réussie, l'image Docker est poussée vers votre compte sur Docker Hub avec `docker push monapp:latest`. Le tag `latest` est utilisé ici à titre d'exemple ; dans un cas d'utilisation réel, il est recommandé de gérer les versions de votre image avec des tags plus spécifiques pour mieux contrôler les déploiements.

Assurez-vous que les secrets `DOCKER_USERNAME` et `DOCKER_PASSWORD` sont bien configurés dans les paramètres de votre dépôt GitHub pour que ces commandes fonctionnent correctement. Cette approche renforce la sécurité de votre workflow en évitant l'exposition de vos identifiants Docker Hub.

## Résumé

1. **Préparation** : Commencez par créer un `Dockerfile` dans votre projet qui décrit l'environnement d'exécution de votre application.

2. **Sécurité** : Configurez les secrets GitHub (`DOCKER_USERNAME` et `DOCKER_PASSWORD`) pour stocker de manière sécurisée vos identifiants Docker Hub.

3. **Workflow GitHub Actions** :

   - **Étape 1** : Utilisez `actions/checkout@v2` pour extraire le code de votre dépôt.
   - **Étape 2** : Construisez votre image Docker en utilisant `docker build`.
   - **Étape 3** : Connectez-vous à Docker Hub avec `docker login` en utilisant les secrets GitHub pour vos identifiants.
   - **Étape 4** : Poussez l'image construite vers Docker Hub avec `docker push`.

4. **Déploiement** : En option, déployez l'image Docker sur votre serveur ou plateforme d'hébergement en exécutant les commandes nécessaires via SSH ou tout autre mécanisme d'orchestration de conteneurs.

5. **Bonnes Pratiques** :
   - Assurez la sécurité de vos informations d'identification en utilisant des secrets GitHub.
   - Utilisez des tags d'image pour gérer les versions de votre application.
   - Intégrez des tests automatiques dans votre workflow pour maintenir la qualité du code.
