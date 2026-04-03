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
┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│ Excel RH │ ──▶ │ Producer │ ──▶ │ Kafka │
│ │ │ (Python) │ │ (Redpanda) │
└─────────────┘ └─────────────┘ └──────┬──────┘
│
▼
┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│ Power BI │ ◀── │ PostgreSQL │ ◀── │ Consumer │
│ │ │ │ │ (Python) │
└─────────────┘ └─────────────┘ └─────────────┘

text

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

```bash
git clone <url-du-projet>
cd Sport-data-solution
2. Créer l'environnement virtuel
bash
python -m venv venv
venv\Scripts\activate      # Windows
source venv/bin/activate   # Linux / Mac
3. Installer les dépendances
bash
pip install -r requirements.txt
4. Démarrer les conteneurs Docker
bash
docker start redpanda
docker start postgres
Exécution du pipeline
Étape 1 – Pipeline batch (génération initiale)
bash
python pipeline.py
Fichiers générés :

data/processed/final_dataset.csv

data/processed/strava_activities.csv

data/processed/slack_messages.csv

data/monitoring/monitoring_report.json

Étape 2 – Streaming Kafka
Terminal 1 – Consumer

bash
python strava_consumer_csv.py
Terminal 2 – Producer

bash
python src/streaming/strava_producer.py
Étape 3 – Import dans PostgreSQL
bash
python import_csv_to_postgres.py
Étape 4 – Visualisation Power BI
Ouvrir Power BI Desktop

Obtenir des données → PostgreSQL

Renseigner :

Serveur : localhost

Base : strava

Utilisateur : postgres

Mot de passe : postgres

Importer la table athlete_stats

Créer les dashboards

Règles métier
python
# Prime 5% : au moins une activité sportive
bonus_eligible = (total_distance_km > 0)

# 5 jours bien-être : 15 activités minimum
wellbeing_eligible = (nb_activities >= 15)
Résultats obtenus
Indicateur	Valeur
Athlètes uniques	116
Total d'activités	56 060
Distance totale	25 478 km
Taux éligibles prime	100 %
Taux éligibles bien-être	45 %
Commandes utiles
Vérifier PostgreSQL
bash
docker exec -it postgres psql -U postgres -d strava -c "SELECT COUNT(*) FROM athlete_stats;"
Voir les messages Kafka
bash
docker exec -it redpanda rpk topic consume strava.activities --offset 0 --num 5
Voir les logs des conteneurs
bash
docker logs postgres
docker logs redpanda
Dépendances principales
text
pandas
kafka-python
psycopg2-binary
sqlalchemy
faker
python-dotenv
googlemaps
openpyxl
Auteurs
Juliette – Marathonienne, cofondatrice

Alexandre – Cycliste, cofondateur

Équipe Data – Développement du POC

Prochaines étapes
📢 Annonce des avantages aux équipes

🔌 Déploiement réel via API Strava

📊 Mise en production avec monitoring

👥 Ouverture Power BI aux managers RH

🎮 Gamification (challenges, classements)

Remerciements
Merci à toute l'équipe pour son engagement en faveur du sport et du bien-être au travail 🚀

text

Ce README est maintenant prêt à être :
1. Copié-collé dans votre fichier `README.md`
2. Commité et pushé sur GitHub
3. Affiché proprement sur la page de votre repository
