# Architechture-de-donnees-automatisee
POC de data engineering pour encourager le sport en entreprise via un système d’avantages. Pipeline complète : ingestion de données RH et sportives, traitement Python, streaming Kafka (Redpanda), stockage PostgreSQL et visualisation Power BI. Détection des collaborateurs éligibles et analyse de l’impact financier.


## Sport Data Solution – POC Avantages Sportifs

## Contexte

Sport Data Solution souhaite encourager la pratique sportive de ses collaborateurs en mettant en place un système de récompenses :

| Avantage | Condition |
|----------|-----------|
| **Prime de 5%** sur le salaire annuel brut | Venir au bureau en faisant du sport (vélo, course, marche, trottinette) |
| **5 jours "bien-être"** par an | Activité physique soutenue (≥ 15 activités par an) |

### Objectifs du POC

-  Tester la faisabilité technique
-  Identifier les données nécessaires
-  Calculer l'impact financier pour l'entreprise

---

## Architecture technique

![Architecture du pipeline](C:/Users/khali/Downloads/Git%20Workflow%20Commit%20Pipeline-2026-04-03-105554.png)

### Composants utilisés

| Composant | Rôle |
|-----------|------|
| **Python** | Extraction, simulation et traitement |
| **Kafka (Redpanda)** | Streaming et découplage des données |
| **PostgreSQL** | Stockage persistant |
| **Power BI** | Visualisation et dashboards |
| **Docker** | Conteneurisation |

---

## Structure du projet

Sport-data-solution/

├── data/

│ ├── raw/

│ │ ├── Donnees_RH.xlsx

│ │ └── Donnees_Sportive.xlsx

│ └── processed/

│ ├── final_dataset.csv

│ ├── strava_activities.csv

│ └── slack_messages.csv

├── src/

│ ├── extract/

│ │ └── extract_excel.py

│ ├── transform/

│ │ ├── clean_rh.py

│ │ ├── calculate_distance.py

│ │ ├── simulate_strava.py

│ │ ├── business_rules.py

│ │ └── slack_generator.py

│ ├── streaming/

│ │ └── strava_producer.py

│ └── monitoring/

│ └── monitoring.py

├── pipeline.py

├── strava_consumer_csv.py

├── import_csv_to_postgres.py

└── requirements.txt

text

---

## Installation

### 1. Cloner le projet

```
- git clone <url-du-projet>

- cd Sport-data-solution
```
### 2. Créer l'environnement virtuel

```
- python -m venv venv
- venv\Scripts\activate      # Windows
- source venv/bin/activate   # Linux / Mac
```

### 3. Installer les dépendances

```
pip install -r requirements.txt
```

### 4. Démarrer les conteneurs Docker
```
- docker start redpanda
- docker start postgres
```
## Exécution du pipeline

### Étape 1 – Pipeline batch (génération initiale)

python pipeline.py

**Fichiers générés :**
```
- data/processed/final_dataset.csv

- data/processed/strava_activities.csv

- data/processed/slack_messages.csv

- data/monitoring/monitoring_report.json
```

 ### Étape 2 – Streaming Kafka

**Terminal 1 – Consumer**

```
python strava_consumer_csv.py
```

**Terminal 2 – Producer**
```
python src/streaming/strava_producer.py
```

### Étape 3 – Import dans PostgreSQL
```
python import_csv_to_postgres.py
```

### Étape 4 – Visualisation Power BI

**Ouvrir Power BI Desktop**

**Obtenir des données → PostgreSQL**

Renseigner :

- Serveur : localhost

- Base : strava

- Utilisateur : postgres

- Mot de passe : xxxxxxx

- Importer la table athlete_stats

- Créer les dashboards


# 👤 Owner

<h1 align="center">Hi 👋, I'm khalid</h1>
<h3 align="center"> Data & Cloud Engineer|| Power BI and Qlik sense developer</h3>

Ce projet a été réalisé par :

**khalid OURO-ADOYI**  

📧 Email : khalidouroadoyi@gmail.com
🔗 [LinkedIn](https://www.linkedin.com/in/khalid-ouro-adoyi/) | [GitHub](https://github.com/LIDONI)
- 📫 How to reach me **khalidouroadoyi@gmail.com**

- 👨‍💻 All of my projects are available at [https://github.com/lidoni?tab=repositories](https://github.com/lidoni?tab=repositories)

- 📄You can see my presentations in my linkedin posts [https://www.linkedin.com/in/khalid-ouro-adoyi/](https://www.linkedin.com/in/khalid-ouro-adoyi/)
