# 📘 Synthèse CI/CD & GitHub Actions

## 🧩 Module 1.1 – Introduction à la CI/CD

### 🎯 Objectifs pédagogiques

- Comprendre les concepts fondamentaux de la CI/CD.
- Identifier les étapes d’une pipeline CI/CD.
- Reconnaître le rôle de Git dans les processus d’intégration et de livraison continues.

### 💡 Contenu

1. **Planification**

   - Utilisation d’outils comme Jira pour créer et gérer des tickets.
   - Attribution des tâches aux membres de l’équipe.
   - Suivi de l’avancement dans une logique projet structurée.

2. **Intégration Continue (CI)**

   - Détection immédiate d’erreurs lors des commits.
   - Exécution automatique de tests unitaires, d’intégration ou statiques.
   - Garantit l’intégrité du code à chaque fusion.

3. **Livraison Continue (CD)**

   - Construction automatique de versions prêtes à être déployées.
   - Préparation permanente à une mise en production.

4. **Déploiement Continu (CD)**
   - Déploiement automatique en production dès validation du code.
   - Aucune intervention humaine nécessaire.

### ✅ Résumé

| Étape                     | Objectif principal                                  |
| ------------------------- | --------------------------------------------------- |
| Planification             | Organisation et répartition des tâches              |
| Intégration Continue (CI) | Intégration et validation automatique du code       |
| Livraison Continue (CD)   | Préparation du code à être déployé à tout moment    |
| Déploiement Continu (CD)  | Mise en production automatique, rapide et sécurisée |

## 🔧 Module 1.2 – Outils et technologies CI/CD

### 🎯 Objectifs pédagogiques

- Identifier les principaux outils de CI/CD.
- Comprendre leur rôle dans une stratégie DevOps.
- Savoir quand et comment les utiliser dans un pipeline.

### 🛠️ Catégories d’outils

#### 1. **Gestion de version**

- Permet la traçabilité et la collaboration sur le code source.
- Outils :
  - `Git` (décentralisé)
  - `Subversion (SVN)` (centralisé)
  - `Mercurial`

#### 2. **Serveurs d’intégration continue (CI)**

- Compilation automatique, tests, intégration du code.
- Exécution dans des environnements isolés (VM ou conteneurs).
- Outils :
  - `Jenkins`
  - `GitHub Actions`
  - `GitLab CI`
  - `CircleCI`
  - `Travis CI`

#### 3. **Livraison et déploiement continu (CD)**

- Automatisation du passage du code à l’environnement de production.
- Réduction des erreurs humaines.
- Outils :
  - `Spinnaker`
  - `Argo CD`
  - `Docker`

#### 4. **Orchestration de conteneurs**

- Gestion dynamique des conteneurs selon la charge et les ressources.
- Mise à l’échelle, redondance, haute disponibilité.
- Outils :
  - `Kubernetes`
  - `Docker Swarm`

#### 5. **Monitoring et logging**

- Suivi en temps réel et enregistrement des événements.
- Analyse de performance, détection d’incidents, audit.
- Outils :
  - `Prometheus`
  - `Grafana`
  - `ELK Stack (Elasticsearch, Logstash, Kibana)`

#### 6. **Versionnage sémantique (SemVer)**

- Convention `MAJOR.MINOR.PATCH` :
  - `MAJOR` : changements incompatibles.
  - `MINOR` : nouvelles fonctionnalités rétrocompatibles.
  - `PATCH` : corrections de bugs.

### ✅ Résumé

Outils essentiels pour la mise en œuvre d’une pipeline CI/CD moderne :

- Suivi du code (`Git`)
- Automatisation (CI/CD)
- Conteneurisation et orchestration
- Supervision applicative
- Gestion structurée des versions

## 🚀 Module 2.1 – Introduction à GitHub Actions

### 🎯 Objectifs pédagogiques

- Définir GitHub Actions et son utilité dans le CI/CD.
- Expliquer son intégration dans l’écosystème GitHub.
- Comprendre la gestion des minutes d’exécution.

### 🔍 Définition

GitHub Actions est un outil d’automatisation intégré à GitHub permettant de créer des workflows CI/CD directement dans les dépôts GitHub, en réponse à des événements (push, PR, tag, cron, etc.).

### 🧩 Écosystème GitHub exploité par GitHub Actions

- **Repositories Git**
- **Pull Requests / Code Review**
- **GitHub Issues**
- **GitHub Pages**
- **GitHub Marketplace** (actions réutilisables)
- **GitHub Security** (scans automatiques)
- **Explore**

### 📈 Cas d’usage

- Automatisation des tests.
- Déploiement automatique (ex : GitHub Pages, cloud).
- Création d’issues à partir de logs d’exécution.
- Intégration avec d'autres services GitHub et sécurité renforcée.

### 🕒 Gestion des minutes d'exécution

#### Fonctionnement

- Crédit gratuit selon plan (public/privé).
- Décompte basé sur l’OS utilisé (Linux < macOS < Windows).

#### Optimisation

- Minimiser les étapes inutiles.
- Déclencher uniquement sur les événements pertinents.
- Utiliser des runners auto-hébergés pour réduire les coûts.

#### Suivi

- Dashboard GitHub pour la consommation.
- Alertes configurables.

### ✅ Résumé

GitHub Actions permet l’automatisation complète du cycle CI/CD au sein de GitHub, avec une gestion fine des ressources et une intégration étroite avec tous les services natifs de la plateforme.

## ⚙️ Module 2.2 – Composants de GitHub Actions

### 🎯 Objectifs pédagogiques

- Identifier les éléments d’un workflow GitHub Actions.
- Comprendre la structuration YAML.
- Maîtriser l’utilisation des runners, actions, jobs, steps.

### 🗂️ Composants

#### 1. **Workflows**

- Définis via des fichiers `.yml` dans `.github/workflows/`
- Déclenchés par des événements : `push`, `pull_request`, `schedule`, etc.

#### 2. **Jobs**

- Groupes de steps exécutés sur un même runner.
- Exécution séquentielle ou parallèle.

#### 3. **Steps**

- Instructions exécutées dans un job.
- Types :
  - Commandes shell (`run`)
  - Actions réutilisables (`uses`)

#### 4. **Actions**

- Modules réutilisables encapsulant des scripts.
- Disponibles sur :
  - `GitHub Marketplace`
  - Définies localement ou via une URL

#### 5. **Runners**

- Machines d’exécution :
  - **Hébergés par GitHub** (Linux, macOS, Windows)
  - **Auto-hébergés** (serveurs personnalisés, VM internes)

### 🧱 Arborescence de GitHub Actions

```zsh
GitHub Actions
├── Workflows
│ ├── Jobs
│ │ ├── Steps
│ │ │ ├── Actions
│ │ │ └── Commandes shell
│ │ └── Runners
│ └── Déclencheurs d'événements
│ ├── push
│ ├── pull_request
│ └── schedule
└── GitHub Marketplace (pour trouver des actions)
```

# 📚 Conclusion

- La CI/CD structure le cycle de vie logiciel en automatisant l’intégration, la livraison et le déploiement.
- Les outils CI/CD couvrent tout l’écosystème DevOps : gestion de version, build/test, conteneurs, déploiement, supervision.
- GitHub Actions fournit une solution CI/CD native et modulaire dans GitHub, parfaitement adaptée aux workflows modernes.
- Une bonne structuration des workflows et une optimisation des ressources sont essentielles pour tirer pleinement parti de GitHub Actions.
