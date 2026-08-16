# 🤖 Machine Learning — Travaux pratiques

Recueil de **travaux pratiques (TP) de Machine Learning** réalisés en Python avec
`scikit-learn`. Le dépôt regroupe, sous forme de *notebooks* Jupyter, un parcours
complet allant des bases (régression, classification, clustering) jusqu'à des cas
d'usage appliqués à la finance (scoring de crédit, robo-advisor, signaux de trading).

> **À qui s'adresse ce dépôt ?** À toute personne qui découvre le Machine Learning
> et veut voir, sur des exemples concrets et commentés, le déroulé complet d'un
> projet : chargement des données → exploration → préparation → modélisation →
> évaluation → interprétation.

---

## 🗂️ Structure du projet

```
machine-learning/
│
├── Intro_ml/                     # 🟢 Les fondamentaux du ML
│   ├── regression.ipynb          # Régression linéaire / multiple / polynomiale
│   ├── Regression1.ipynb         # Même sujet, version « au propre »
│   ├── Classification.ipynb      # Classification (Régression logistique + kNN)
│   ├── Non superviser.ipynb      # Apprentissage non supervisé (K-Means, CAH)
│   ├── maisons_taiwan.csv        # Jeu de données : prix de logements (Taïwan)
│   └── billets.csv               # Jeu de données : billets vrais / faux
│
├── TP1.ipynb                     # 🔵 Prédiction du prix de l'immobilier (Californie)
├── TP1 Decision Tree.ipynb       # 🔵 Arbre de décision : accord de prêt bancaire
├── TP2.ipynb                     # 🔵 Robo-advisor : tolérance au risque d'un investisseur
├── TP BTC.ipynb                  # 🔵 Signaux d'achat/vente sur le Bitcoin
│
├── datasets/housing/housing.csv  # Données immobilier californien (pour TP1)
├── SCFP2009panel.xlsx            # Données Survey of Consumer Finances (pour TP2)
│
└── README.md                     # Ce fichier
```

🟢 = niveau introductif  🔵 = niveau appliqué / avancé

---

## 📚 Contenu détaillé des notebooks

### 🟢 Les fondamentaux — dossier `Intro_ml/`

| Notebook | Type de problème | Ce qu'on y apprend |
|----------|------------------|--------------------|
| **regression.ipynb** / **Regression1.ipynb** | Régression (supervisé) | Prédire le **prix d'un logement** à Taïwan à partir de son âge, de sa distance au métro et au commerce. On y voit la régression **linéaire simple**, **multiple** et **polynomiale**, avec évaluation par **RMSE** et **R²**. |
| **Classification.ipynb** | Classification binaire (supervisé) | Détecter si un **billet est authentique ou faux** à partir de ses dimensions (`billets.csv`). Comparaison de deux modèles : **Régression logistique** et **k plus proches voisins (kNN)**, évaluation via matrice de confusion, précision et rappel. |
| **Non superviser.ipynb** | Clustering (non supervisé) | Regrouper des points sans étiquette avec **K-Means**, choisir le bon nombre de groupes avec la **méthode du coude**, puis explorer la **classification hiérarchique** (dendrogramme) et le **score de silhouette**. |

### 🔵 Cas appliqués — racine du dépôt

#### `TP1.ipynb` — Prédiction du prix de l'immobilier californien
Le TP « fil rouge » qui déroule **toute la chaîne d'un projet de régression** sur le
célèbre jeu de données *California Housing* :
- Cadrage métier (tâche supervisée, choix de la métrique **RMSE vs MAE**) ;
- Exploration et visualisation (histogrammes, carte géographique, corrélations) ;
- **Échantillonnage stratifié** pour un jeu de test représentatif (éviter le *data leakage*) ;
- **Feature engineering** (pièces par foyer, ratio de chambres…) ;
- **Pipeline de préparation** (imputation des valeurs manquantes, encodage *one-hot*, mise à l'échelle) ;
- Comparaison de modèles : *baseline*, **Régression linéaire**, **Arbre de décision**, **Random Forest**, **SVR**, **réseau de neurones (MLP)** ;
- **Validation croisée**, analyse **biais / variance** et **GridSearch** pour l'optimisation.

#### `TP1 Decision Tree.ipynb` — Accord de prêt bancaire
Classification binaire (prêt **accordé / refusé**) avec un **arbre de décision** :
exploration des données, matrice de corrélation, entraînement, **visualisation de
l'arbre**, importance des variables, frontière de décision. Le notebook aborde aussi
un point **d'éthique** (pourquoi le genre ne doit pas influencer une décision de crédit).

#### `TP2.ipynb` — Robo-advisor : tolérance au risque
On construit une cible « **TrueRiskTolerance** » (part d'actifs risqués d'un ménage)
à partir des données *Survey of Consumer Finances* (`SCFP2009panel.xlsx`), avant et
après la crise de 2008. Objectif : **prédire la tolérance au risque d'un investisseur**
à partir de ses seules caractéristiques de 2007 (âge, revenu, patrimoine…), en évitant
le *data leakage*. Sélection de variables, comparaison de modèles, **GridSearch**,
importance des variables et **sauvegarde du modèle** (`pickle`) pour un futur tableau de bord.

#### `TP BTC.ipynb` — Signaux de trading sur le Bitcoin
Classification **Achat (1) / Vente (0)** de minutes de cotation du Bitcoin :
- Création du label via **croisement de moyennes mobiles** (courte vs longue) ;
- **Feature engineering** d'indicateurs techniques (EMA, RSI, ROC, Momentum…) ;
- **Réduction de dimension** (SVD) et visualisation **t-SNE** ;
- Comparaison de nombreux algorithmes, **GridSearch** sur Random Forest ;
- **Backtesting** de la stratégie (avec `shift(1)` pour éviter le biais de prévision).

> ℹ️ `module3.ipynb` est un fichier vide (placeholder) et peut être ignoré.

---

## 📦 Jeux de données

| Fichier | Lignes | Description | Utilisé par |
|---------|--------|-------------|-------------|
| `Intro_ml/maisons_taiwan.csv` | ~414 | Transactions immobilières à Taïwan (`age`, `metro`, `epicerie`, `prix`…) | `regression*.ipynb` |
| `Intro_ml/billets.csv` | ~1 500 | Dimensions de billets (`length`, `margin_low`… + `is_genuine`), **séparateur `;`** | `Classification.ipynb` |
| `datasets/housing/housing.csv` | ~20 640 | California Housing (revenus, position, valeur médiane…) | `TP1.ipynb` |
| `SCFP2009panel.xlsx` | — | Survey of Consumer Finances 2009 (panel 2007/2009) | `TP2.ipynb` |

> ⚠️ Deux notebooks téléchargent leurs données à l'exécution :
> **`TP1.ipynb`** récupère le dataset housing depuis le dépôt d'Aurélien Géron, et
> **`TP BTC.ipynb`** télécharge les données Bitcoin via `kagglehub` (compte Kaggle requis).
> Le notebook **`TP1 Decision Tree.ipynb`** attend un fichier `loan_data.csv` qui
> **n'est pas fourni** dans le dépôt (voir « Limitations » plus bas).

---

## 🚀 Installation & exécution

### 1. Prérequis
- **Python 3.10+** (le projet a été développé sous Python 3.12)
- `pip` et, idéalement, un environnement virtuel

### 2. Cloner le dépôt
```bash
git clone https://github.com/Kingu2807/machine-learning.git
cd machine-learning
```

### 3. Créer un environnement virtuel et installer les dépendances
```bash
# Créer et activer l'environnement
python -m venv .venv
source .venv/bin/activate      # sous Windows : .venv\Scripts\activate

# Installer les bibliothèques
pip install -r requirements.txt
```

### 4. Lancer Jupyter
```bash
jupyter lab      # ou : jupyter notebook
```
Ouvrez ensuite le notebook souhaité et exécutez les cellules de haut en bas.

---

## 🧰 Bibliothèques utilisées

`pandas` · `numpy` · `scikit-learn` · `matplotlib` · `seaborn` · `scipy` ·
`openpyxl` (lecture Excel) · `graphviz` (visualisation d'arbre) ·
`kagglehub` (téléchargement du dataset BTC) · `jupyterlab`

---

## ⚠️ Limitations & pistes d'amélioration

Pour toute personne qui reprend ce dépôt, quelques points à connaître :

- **Chemins absolus en dur** : `TP1 Decision Tree.ipynb` contient des chemins de type
  `/Users/guillaume/...`. Il faut les remplacer par des chemins relatifs et fournir
  le fichier `loan_data.csv` pour que le notebook s'exécute.
- **Environnement virtuel versionné** : le dossier `.venv312/` (≈ 847 Mo) a été
  committé par erreur. Il ne devrait **pas** figurer dans Git — le `.gitignore`
  fourni ici l'exclut désormais. Pour l'enlever de l'historique :
  ```bash
  git rm -r --cached .venv312
  git commit -m "Retire l'environnement virtuel du suivi Git"
  ```
- **`module3.ipynb`** est vide et peut être supprimé.
- **Doublon** : `regression.ipynb` et `Regression1.ipynb` traitent le même sujet ;
  on peut n'en garder qu'un.

---

## 📄 Contexte

Notebooks pédagogiques réalisés dans le cadre d'un cours de **Machine Learning**.
Chaque notebook alterne code, visualisations et cellules « **Stop & think** » qui
répondent aux questions de compréhension — un bon support pour réviser ou apprendre.
