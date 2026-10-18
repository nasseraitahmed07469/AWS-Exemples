# AWS-Exemples

Dépôt de travail pour apprendre Amazon Web Services et préparer la certification **AWS Certified Solutions Architect – Associate (SAA-C03)**.

L’objectif est de rassembler progressivement des exemples et des travaux pratiques pour comprendre les services AWS, leurs cas d’usage et les choix d’architecture associés.

## État du dépôt

Le dépôt contient actuellement ce guide et une configuration Dev Container basée sur Ubuntu. Les exercices et les exemples de code restent à ajouter. Aucune infrastructure AWS n’est déployée automatiquement.

```text
AWS-Exemples/
├── .devcontainer/
│   └── devcontainer.json   # Environnement de développement Ubuntu
└── README.md              # Présentation et guide de démarrage
```

## Prérequis

- Git pour récupérer le dépôt.
- Python 3 et le module `venv` pour installer AWS CLI dans un environnement isolé.
- Pour travailler dans le Dev Container : Visual Studio Code, l’extension Dev Containers et Docker en cours d’exécution.
- Pour les exercices connectés : un compte AWS, une authentification valide et les autorisations nécessaires.

Les exemples hors ligne ci-dessous ne nécessitent pas de compte AWS.

## Démarrage rapide

### Récupérer le dépôt

```bash
git clone https://github.com/nasseraitahmed07469/AWS-Exemples.git
cd AWS-Exemples
```

Dans l’environnement cloud Codex, utilisez directement le checkout existant :

```bash
cd /workspace/AWS-Exemples
```

### Utiliser le Dev Container (facultatif)

Ouvrez le dossier dans Visual Studio Code, puis lancez **Dev Containers: Reopen in Container** depuis la palette de commandes.

La configuration actuelle fournit une base Ubuntu ; elle n’installe pas automatiquement AWS CLI.

### Installer AWS CLI

Sous Linux ou dans le Dev Container, créez un environnement Python à l’extérieur du dépôt :

```bash
python3 -m venv "$HOME/.venvs/aws-lab"
source "$HOME/.venvs/aws-lab/bin/activate"
python -m pip install awscli==1.45.29
python -m pip check
aws --version
```

Cette procédure installe **AWS CLI v1**. Pour les fonctionnalités propres à AWS CLI v2, notamment les parcours d’authentification avec IAM Identity Center, utilisez le [guide officiel d’installation](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

Dans l’environnement cloud préparé pour ce dépôt, AWS CLI est déjà installé. Activez-le dans chaque nouveau terminal :

```bash
source /workspace/.venvs/aws-lab/bin/activate
aws --version
```

## Premiers exemples sans connexion AWS

Générez des modèles d’entrée JSON pour explorer les paramètres des services :

```bash
# Paramètres d’une demande de lancement d’instance EC2
aws ec2 run-instances --generate-cli-skeleton input

# Paramètres d’une demande de création de bucket S3
aws s3api create-bucket --generate-cli-skeleton input
```

Avec `--generate-cli-skeleton input`, ces commandes ne contactent pas AWS et ne créent aucune ressource. Les valeurs générées servent de modèles et doivent être adaptées avant toute utilisation réelle.

## Se connecter à AWS

Configurez une authentification adaptée à votre compte en suivant le [guide AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-authentication.html). Privilégiez des identifiants temporaires et des permissions limitées aux besoins de l’exercice.

Une fois l’authentification disponible, vérifiez l’identité utilisée :

```bash
aws sts get-caller-identity
```

Cette commande appelle AWS et affiche le compte ainsi que l’identité courante. Ne partagez pas sa sortie publiquement sans en masquer les informations de compte.

Choisissez également une région adaptée à vos exercices, par exemple pour le terminal courant :

```bash
export AWS_DEFAULT_REGION=eu-west-3
```

Ne placez jamais de clés d’accès, de jetons ou de fichiers d’identifiants dans le dépôt. Utilisez les mécanismes d’authentification AWS et les paramètres sécurisés de votre environnement.

## Parcours d’étude suggéré

Les sujets suivants constituent une feuille de route ; ils ne correspondent pas encore à des exercices présents dans le dépôt.

| Thème | Services et notions à explorer |
| --- | --- |
| Identité et sécurité | IAM, rôles, politiques, moindre privilège, KMS |
| Réseau | VPC, sous-réseaux, tables de routage, Security Groups |
| Calcul | EC2, Elastic Load Balancing, Auto Scaling, Lambda |
| Stockage | S3, EBS, EFS, classes de stockage et cycle de vie |
| Bases de données | RDS, Aurora, DynamoDB, sauvegarde et disponibilité |
| Résilience et performance | Zones de disponibilité, CloudFront, Route 53 |
| Supervision et coûts | CloudWatch, CloudTrail, AWS Budgets |

Pour chaque exercice, documentez l’objectif, les prérequis, les étapes, le résultat attendu et les commandes de nettoyage.

## Coûts et nettoyage

Les manipulations dans un compte AWS peuvent engendrer des frais, y compris lorsque certaines offres gratuites s’appliquent. Vérifiez les tarifs, configurez des alertes de budget et supprimez les ressources devenues inutiles après chaque exercice. Une alerte de budget ne bloque pas automatiquement les dépenses.

## Vérifications disponibles

Le dépôt ne dispose pas encore de suite de tests automatisés ni d’application à démarrer. Pour vérifier la préparation locale, utilisez `aws --version`, `python -m pip check` et les deux commandes de génération de modèles ci-dessus.

Ces vérifications valident l’installation et le fonctionnement hors ligne de la CLI. L’accès à un compte AWS se vérifie séparément avec une authentification valide.

## Ressources utiles

- [Certification AWS Solutions Architect – Associate](https://aws.amazon.com/certification/certified-solutions-architect-associate/)
- [Documentation AWS](https://docs.aws.amazon.com/)
- [Référence AWS CLI](https://docs.aws.amazon.com/cli/latest/reference/)
- [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html)
- [Tarification AWS](https://aws.amazon.com/pricing/)
