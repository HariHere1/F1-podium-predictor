# 🏎️ F1 Podium Predictor

A machine learning project that predicts which drivers will finish on the podium (top 3) in Formula 1 races, based on historical race results and qualifying data.

## 📌 Overview

Formula 1 podium finishes are influenced by a mix of car performance, driver skill, grid position, and track characteristics. This project explores historical F1 data to build a model that predicts podium outcomes for each driver in a race.

The work is currently developed as a Jupyter notebook (`notebook.ipynb`), covering the initial data exploration stage: loading the datasets, merging race results with race metadata, filtering to modern-era seasons (2010+), and labeling podium finishers (finishing position ≤ 3).

## 📊 Dataset

The `data/` folder contains CSV files in the [Ergast Developer API](https://ergast.com/mrd/) database format:

| File | Description |
|---|---|
| `results.csv` | Race results for every driver in every race (finishing position, laps, time, points…) |
| `races.csv` | Race calendar metadata (raceId, year, round, circuitId, etc.) |
| `qualifying.csv` | Qualifying session results (grid positions, lap times in Q1/Q2/Q3) |
| `drivers.csv` | Driver details (name, nationality, date of birth, driverRef) |
| `constructors.csv` | Constructor (team) details |
| `circuits.csv` | Circuit details (location, country, coordinates) |

**Preprocessing done so far:**

1. Merge `results.csv` with `races.csv` (on `raceId`) to attach `year`, `round`, and `circuitId` to each result.
2. Keep only races from **2010 onwards** to reflect the modern hybrid-era sporting landscape.
3. Create a target label where a finisher is on the podium if `positionOrder <= 3`.

## 🧰 Tech Stack

- **Python 3** — core language
- **pandas / NumPy** — data loading, merging, and wrangling
- **scikit-learn** — modeling (planned)
- **matplotlib / seaborn** — visualization (planned)
- **Jupyter Notebook** — development environment

## 🚀 Getting Started

1. **Clone the repository**

   ```bash
   git clone https://github.com/<your-username>/F1-podium-predictor.git
   cd F1-podium-predictor
   ```

2. **Create and activate a virtual environment**

   ```bash
   python -m venv venv
   venv\Scripts\activate        # Windows (PowerShell / cmd)
   source venv/bin/activate     # macOS / Linux
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Launch Jupyter and open the notebook**

   ```bash
   jupyter notebook
   ```

   Then open `notebook.ipynb`. Data paths are relative to the project root (e.g. `data/results.csv`), so run the notebook from the project root.

## 📁 Project Structure

```
F1-podium-predictor/
├── data/                  # Ergast CSV datasets (results, races, qualifying, drivers, …)
├── notebook.ipynb         # Main analysis and modeling notebook
├── requirements.txt       # Python dependencies
├── README.md              # This file
└── venv/                  # Local virtual environment (not committed)
```

## 🗺️ Roadmap

- [x] Load and inspect the Ergast CSV datasets
- [x] Merge results with race metadata, filter seasons ≥ 2010
- [x] Define the podium target (`positionOrder <= 3`)
- [ ] Feature engineering (grid position, qualifying times, driver/constructor form, circuit history)
- [ ] Train baseline classifiers (e.g. Logistic Regression, Random Forest, Gradient Boosting)
- [ ] Evaluate with appropriate metrics (recall / PR-AUC — podium finishes are a small fraction of all entries)
- [ ] Predict podiums for upcoming races

## 📝 Notes

- `positionOrder` reflects the **official finishing classification** (including penalties), not just crossing position.
- Podium finishes are rare relative to all race entries, so class imbalance should be handled thoughtfully in later modeling stages.

## 📄 License

TBD — add your preferred license before publishing.
