# Les secrets dans GitHub

## Exemple d'un secret avec un VPS

```yaml
name: Deploy to VPS

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Vérification du code
        uses: actions/checkout@v4

      - name: Copie des fichiers de configuration
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.VPS_HOST }}
          username: "votre_user"
          key: ${{ secrets.SSH_KEY }}
          script: |
            cd /path/to/your/app
            git pull
            ./deploy.sh
```

### Explications

- `SSH_KEY` : Votre clé privée SSH, utilisée pour établir une connexion sécurisée au VPS sans exposer votre mot de passe.
- `VPS_HOST` : L'adresse de votre serveur VPS, permettant à GitHub Actions de savoir où se connecter.
- `appleboy/ssh-action` est une action GitHub qui permet d'établir une connexion SSH à un serveur distant directement depuis un workflow GitHub Actions. Cette action simplifie l'exécution de commandes SSH sur un serveur distant, ce qui est idéal pour déployer des applications, exécuter des scripts, ou effectuer des tâches de maintenance à distance.
- `deploy.sh` mentionné dans l'exemple de workflow est un script shell que vous devriez avoir sur votre VPS. Ce script contient les commandes nécessaires pour déployer ou mettre à jour votre application sur le serveur. L'utilisation d'un script de déploiement permet de centraliser et de standardiser le processus de déploiement, garantissant que toutes les étapes nécessaires sont exécutées de manière cohérente.

## Explication du `deploy.sh`

L'exemple suivant suppose que vous avez une application web simple que vous souhaitez mettre à jour et redémarrer sur votre serveur VPS.

```bash
# Naviguer dans le répertoire de votre application
cd /path/to/your/app

# Mettre à jour le code source
# Supposons que votre code est hébergé sur un dépôt Git
git pull origin main

# Installer les dépendances
# Exemple pour une application Node.js
npm install

# Construire votre projet si nécessaire
# Exemple pour une application construite avec un outil comme webpack
npm run build

# Redémarrer le serveur
# Cela dépend de la manière dont votre application est servie
# Exemple pour une application Node.js utilisant pm2
pm2 restart app_name

# Pour d'autres types d'applications, vous pouvez avoir besoin de commandes spécifiques
# Exemple pour redémarrer un service systemd
# systemctl restart my_application.service

echo "Déploiement terminé"
```

Ce script effectue les actions suivantes :

1. **Navigation** : Se déplace dans le répertoire où votre application est située sur le serveur.
2. **Mise à jour du code** : Utilise `git pull` pour mettre à jour le code de l'application à la dernière version disponible sur la branche principale.
3. **Installation des dépendances** : Exécute `npm install` pour s'assurer que toutes les dépendances nécessaires sont installées ou mises à jour.
4. **Construction du projet** : Pour les applications qui nécessitent une étape de construction, `npm run build` est exécuté.
5. **Redémarrage du serveur/application** : Utilise `pm2` pour redémarrer l'application Node.js. Si vous utilisez un autre système pour servir votre application, vous aurez besoin d'adapter cette partie du script à vos besoins (par exemple, en utilisant `systemctl restart` pour un service systemd).

Assurez-vous de modifier le script en fonction de l'environnement spécifique de votre serveur et des exigences de votre application. Par exemple, si votre application est une application Python utilisant Gunicorn et Nginx, les commandes de redémarrage et de construction seront différentes.

## Résumé

1. **Introduction aux Secrets** : Les secrets permettent de stocker des informations sensibles, telles que des mots de passe, des jetons d'accès, ou des clés SSH, de manière sécurisée dans GitHub. Ils sont essentiels pour protéger vos données et configurations sensibles lors de l'automatisation des workflows CI/CD.

2. **Utilisation Pratique des Secrets** :

   - Pour sécuriser la communication avec un serveur VPS dans un workflow GitHub Actions, les secrets tels que `SSH_KEY` et `VPS_HOST` sont utilisés pour stocker respectivement votre clé privée SSH et l'adresse de votre serveur VPS.
   - Un exemple de fichier de workflow, `deploy.yml`, montre comment ces secrets peuvent être intégrés pour déployer une application sur un VPS de manière sécurisée.

3. **`appleboy/ssh-action`** : Cette action GitHub est utilisée pour établir une connexion SSH sécurisée avec un serveur distant, permettant l'exécution de commandes pour le déploiement ou la maintenance. L'utilisation de cette action dans votre workflow facilite l'automatisation des déploiements tout en maintenant la sécurité grâce à l'usage de secrets.

4. **Le Script de Déploiement `deploy.sh`** :
   - Un script shell côté serveur qui contient les commandes nécessaires pour mettre à jour et redémarrer votre application.
   - Le script est invoqué dans le workflow GitHub Actions, démontrant comment les tâches de déploiement peuvent être automatisées de manière sécurisée en utilisant des secrets pour gérer les informations d'accès.
