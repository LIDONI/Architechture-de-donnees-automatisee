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

- ✅ Tester la faisabilité technique
- ✅ Identifier les données nécessaires
- ✅ Calculer l'impact financier pour l'entreprise

---

## Architecture technique

![Diagramme des flux](kestra/Diagramme-des-flux.png)

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
