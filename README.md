# Mind-the-crash
# Classificazione della gravità degli incidenti stradali – STATS19

Progetto di gruppo per l'esame di **Statistical Modelling & Machine Learning**.
Analisi e modellazione dei dati **STATS19** del Department for Transport (DfT) sugli incidenti stradali con feriti in Gran Bretagna.

## Obiettivo

Il modello simula un **centralino di emergenza**: usando solo le informazioni disponibili al momento della chiamata (luogo, infrastruttura, contesto, tipo di veicoli e quanto riferito a voce da chi chiama), classifica la collisione come:

| Classe | Valore |
|---|---|
| Fatal / Serious (feriti gravi o mortali) | `1` |
| Slight (feriti lievi) | `0` |

Le variabili note solo dopo l'evento sono escluse. Le motivazioni di ogni esclusione sono documentate nel notebook di preprocessing.

## Dati

I dati **non sono inclusi nel repository** a causa delle dimensioni dei file. Vanno scaricati dal sito del DfT:

👉 [Road Safety Data – data.gov.uk](https://www.data.gov.uk/dataset/cb7ae6f0-4be6-4935-9277-47e5ce24a11f/road-accidents-safety-data)

Dopo il download, organizzali in questa struttura:

```
00_Data/
├── 5_years/              # ultimi 5 anni (dataset usato nel progetto)
│   ├── collision.csv
│   ├── casualty.csv
│   └── vehicle.csv
└── Input/                # generata da 02_Preprocessing (X_train, X_test, y_train, y_test)
```

## Pipeline

| Notebook | Contenuto |
|---|---|
| `01_Analisi.ipynb` | EDA: struttura dei dati, valori mancanti, stagionalità degli incidenti |
| `02_Preprocessing.ipynb` | Pulizia, encoding, feature engineering, split 70/30 stratificato per settimana dell'anno, imputazione (fit solo sul training) |
| `03_Variable_selection.ipynb` | Selezione delle variabili con importanza da Random Forest e regola 1-SE |
| `04_Modelli.ipynb` | Confronto dei modelli (Logistic Regression, Random Forest, XGBoost, MLP, Bagging, Voting) con AUC in CV 5-fold, curve ROC e scelta della soglia |

I notebook vanno eseguiti in ordine, perché ognuno legge gli output di quello precedente.

Il file `Selezione_variabili.xlsx` documenta le scelte fatte su ciascuna variabile.

## Setup

```bash
git clone https://github.com/<utente>/<nome-repo>.git
cd <nome-repo>
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

Principali librerie: `pandas`, `numpy`, `scikit-learn`, `xgboost`, `plotly`, `matplotlib`.

## Team

- Salvatore Zizzi – [@Salvo-zizzi](https://github.com/Salvo-zizzi)
- Joana Curri - [@joanacurri](https://github.com/joanacurri)
- Edy Delcane – @username
- Mario D'Angelo – @username

## Fonti

- Department for Transport, *Road Safety Data (STATS19)*
- DfT, *Reported road casualties Great Britain: economic valuation methodology*
- DfT, guida ai dati storici e al *severity adjustment*
