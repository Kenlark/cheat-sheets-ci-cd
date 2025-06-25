# Création d'un workflow

```yml
name: Exemple de Workflow CI

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
  schedule:
    - cron: `0 2 * *`

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Exécution d'un script simple
      - uses: actions/checkout@v4
        run: echo "Workflow exécuté suite à un push ou une pull request sur la branche main."
```

### Explications :

- **`name`** : Nomme votre workflow. Ici, "Exemple de Workflow CI".
- **`on`** : Définit le ou les événements qui déclencheront le workflow. Dans cet exemple, le workflow se déclenche à chaque `push` et chaque `pull_request`.
- **`jobs`** : Contient un ensemble de jobs à exécuter. Ici, il y a un seul job nommé `build`.
- **`runs-on`** : Spécifie le type de runner que le job doit utiliser. `ubuntu-latest` indique la dernière version d'Ubuntu fournie par GitHub.
- **`steps`** : Étapes à exécuter dans le job.
  - **`uses: actions/checkout@v4`** : Utilise l'action `checkout` pour cloner votre dépôt dans le runner.
  - **`run`** : Exécute une commande shell. Ici, affiche un message dans les logs.
- **`schedule`** : Déclenche le workflow selon un planning défini.
- **`cron`** : La syntaxe cron `'0 2 * * *'` signifie que le workflow s'exécute tous les jours à 2h00 UTC.

### Autres Événements

- **Syntaxe**: `on: <event_name>`
- **Description**: GitHub Actions supporte une variété d'autres événements, tels que `issues`, `release`, et `fork`. Chaque type d'événement permet de déclencher des workflows pour des cas d'usage spécifiques, renforçant l'intégration et l'automatisation dans l'écosystème GitHub.

## Résumé

1. **Push** : Automatisez l'exécution de workflows à chaque fois qu'un commit est poussé vers le dépôt, permettant une intégration continue efficace.

2. **Pull Request** : Utilisez ce déclencheur pour lancer des workflows lorsqu'une action est effectuée sur une Pull Request, facilitant les tests automatisés et les vérifications de code avant la fusion.

3. **Schedule** : Planifiez l'exécution de workflows à des moments précis avec la syntaxe cron, idéal pour les tâches récurrentes comme les mises à jour ou les audits réguliers.

4. **Workflow Dispatch** : Offre la possibilité de déclencher manuellement des workflows depuis GitHub, apportant une flexibilité pour exécuter des tâches à la demande.

5. **Autres Événements** : GitHub Actions prend en charge une large gamme d'événements, vous permettant de créer des workflows personnalisés qui s'adaptent à divers besoins et scénarios d'automatisation.

6. **Configuration d'un Déclencheur** : La configuration des déclencheurs se fait facilement dans le fichier YAML du workflow, vous permettant de spécifier les branches et les conditions sous lesquelles vos workflows doivent s'exécuter.
