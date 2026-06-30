# Devoir 1 : ETE435 Géoinformatique

**Titre :** Ingénierie des données géospatiales : Classe `Aeroports`, LineString, Polygon et analyse de proximité

**Auteurs :**
- Alan CASSEUS, Mémorant en Sciences de l'Environnement (FSTEAT/CHCL-UEH)
- Joscelyn PARFAIT, Diplômé en Génie Civil (FSG/CHCL-UEH)

**Professeur :** Paul Célicourt, PhD en Hydroinformatique  
**Date de soumission :** 29 Juin 2026  
**Institution :** Campus Henry Christophe de l'Université d'État d'Haïti à Limonade (CHC-UEH-L)

## Description

Ce dépôt contient la solution complète du Devoir 1 du cours ETE435 - Géoinformatique. L'objectif est de développer une classe Python `Aeroports` permettant de manipuler et analyser des données géographiques d'aéroports canadiens, en réalisant :

1. **Préparation des données** — nettoyage et validation du CSV source
2. **LineString** — parcours reliant 3 aéroports sélectionnés automatiquement
3. **Polygon** — zone polygonale construite à partir des mêmes aéroports
4. **Analyse spatiale** — vérification qu'un aéroport aléatoire se trouve ou non à l'intérieur du polygone

## Structure du dépôt

```
devoir1-ETE435/
├── devoir1_ETE435.ipynb          # Notebook principal (classe Aeroports)
├── airports_canada_chcl.csv      # Données brutes (417 aéroports)
├── airports_clean.csv            # Données nettoyées (352 aéroports valides)
├── large_airports_canada.geojson # Export GeoJSON (20 grands aéroports)
├── requirements.txt              # Environnement Python reproductible
└── README.md                     # Ce fichier
```

## Résultats du nettoyage

| Étape | Lignes | Action |
|---|---|---|
| Lignes initiales (fichier brut) | 417 | — |
| Coordonnées manquantes / non-numériques | 58 | Supprimées |
| Valeurs aberrantes géographiques | 7 | Supprimées |
| **Lignes valides (airports_clean.csv)** | **352** | **Conservées** |

### Anomalies principales détectées

- **CEL5** : longitude = `'CEL15'` (valeur textuelle au lieu d'un numérique)
- **CAZ5** : longitude = `'ETE435'` (code du cours inséré par erreur)
- **CYVR, CYOW, CYHZ, CYYT, CYQA** : latitude = `-50.567` (valeur aberrante répétée)
- **CYFH** : longitude = `-150.0` (hors des limites canadiennes)
- **CYGZ** : latitude = `92.568` (physiquement impossible — max 90°N)

## Aéroports sélectionnés pour le LineString / Polygon

| Ident | Nom | Latitude | Longitude |
|---|---|---|---|
| CYUL | Montréal-Trudeau International | 45.4678°N | 73.7423°O |
| CYYZ | Toronto Pearson International | 43.6759°N | 79.6294°O |
| CYYC | Calgary International | 51.1188°N | 114.0099°O |

## Résultat de l'analyse de proximité

- **Aéroport aléatoire (seed=42)** : CYFR — Fort Resolution Airport
- **Position** : 61.1808°N, 113.6900°O
- **Résultat** : EXTÉRIEUR du polygone

## Reproductibilité

```bash
# Cloner le dépôt
git clone https://github.com/T-kitt-dan/devoir1-ETE435.git
cd devoir1-ETE435

# Créer et activer l'environnement virtuel
python -m venv venv_devoir1
# Windows :
venv_devoir1\Scripts\activate
# Linux / macOS :
source venv_devoir1/bin/activate

# Installer les dépendances
pip install -r requirements.txt

# Lancer le notebook
jupyter lab devoir1_ETE435.ipynb
```
## Bibliothèques utilisées

| Bibliothèque | Version | Rôle |
|---|---|---|
| pandas | 3.0.1 | Manipulation des données tabulaires |
| geopandas | 1.1.3 | Export GeoJSON et GeoDataFrame |
| shapely | 2.1.2 | Géométries Point, LineString, Polygon |
| folium | 0.20.0 | Visualisation cartographique interactive |
| numpy | 2.4.3 | Calculs numériques |

## Aide externe

- Documentation officielle : pandas, geopandas, shapely, folium
- Assistance IA : Claude (Anthropic) — vérification de la cohérence du pipeline
