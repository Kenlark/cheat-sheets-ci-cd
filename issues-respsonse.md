# Création d'un issue response

```yaml
name: Issue Response

on:
  issues:
    types: [opened]

jobs:
  respond_to_issue:
    runs-on: ubuntu-latest
    steps:
      - name: Send a response
        uses: actions/github-script@v3
        with:
          github-token: ${{secrets.GITHUB_TOKEN}}
          script: |
            github.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: 'Merci pour votre issue, notre équipe va se pencher dessus !'
            })
```

## Explication du Fichier YAML

- **`name`**: Nomme votre workflow, facilitant son identification.
- **`on`**: Définit le déclencheur de l'événement, ici `issues` avec le type `opened`, signifiant que le workflow s'exécute chaque fois qu'une issue est ouverte.
- **`jobs`**: Définit les tâches à exécuter, ici `respond_to_issue`.
- **`runs-on`**: Spécifie le type de runner, `ubuntu-latest` dans ce cas.
- **`steps`**: Les étapes à exécuter dans le job, utilisant ici `actions/github-script` pour exécuter un script permettant de commenter automatiquement la nouvelle issue.
- **`github-token`**: Utilise le token `GITHUB_TOKEN` pour authentifier les actions avec GitHub.
- **`script`**: Le script exécuté pour créer un commentaire sur l'issue, indiquant un message de prise en charge.

## Testez

1. **Poussez** les modifications à votre dépôt.
2. **Ouvrez une nouvelle issue** dans votre dépôt pour déclencher le workflow.
3. **Vérifiez** l'issue pour voir le commentaire automatique posté par GitHub Actions.

## Résumé

1. **Création du Fichier de Workflow** : Commencez par créer un fichier YAML dans le répertoire `.github/workflows` de votre dépôt GitHub, par exemple `issue_response.yml`.

2. **Configuration du Workflow** :

   - **Déclencheur** : Utilisez `on: issues` avec le type `opened` pour activer le workflow lorsque de nouvelles issues sont ouvertes.
   - **Jobs et Steps** : Configurez un job `respond_to_issue` qui exécute des steps utilisant `actions/github-script` pour poster un commentaire automatique sur l'issue ouverte.
   - **Authentification** : Employez `github-token: ${{secrets.GITHUB_TOKEN}}` pour authentifier les interactions avec GitHub via le workflow.

3. **Test du Workflow** :
   - Après avoir poussé le fichier de workflow à votre dépôt, ouvrez une nouvelle issue pour déclencher automatiquement le workflow.
   - Vérifiez que le commentaire automatique est bien posté sur l'issue, confirmant le bon fonctionnement du workflow.
