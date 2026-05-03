# Steam Game Success Analysis

## Repository Structure

```
├── Steam_Data_Collect.ipynb      # Data collection via Steam API
├── Steam_Analysis_with_ML.ipynb  # Full analysis + ML model
├── steam-game-id-list.json       # 30,000 Steam App IDs (input)
└── steam_games_data.csv          # Collected dataset (output)
```

---

## Dataset

The dataset was **self-collected** by scraping three Steam API endpoints for each game:

| Column | Description |
|---|---|
| `AppID` | Unique Steam application ID |
| `Name` | Game title |
| `Price_THB` | Current price in Thai Baht |
| `Initial_Price_THB` | Launch price in Thai Baht |
| `Genres` | Comma-separated genre tags |
| `Total_Reviews` | Total number of user reviews |
| `Positive_Reviews` | Number of positive reviews |
| `Rating_Percent` | Positive review percentage (0–100%) |
| `Windows` | Windows platform support (True/False) |
| `Mac` | macOS platform support (True/False) |
| `Linux` | Linux platform support (True/False) |

## 🔧 Data Collection — `Steam_Data_Collect.ipynb`

The collection script calls **3 API endpoints per game** and supports pause/resume:

```
For each App ID:
  ├── Call 1: store.steampowered.com/api/appdetails?cc=us  →  name, price (USD), platforms, genres
  ├── Call 2: store.steampowered.com/api/appdetails?cc=th  →  initial price (THB)
  └── Call 3: store.steampowered.com/appreviews/{id}       →  total reviews, positive reviews
```

## How to Run

### 1. Collect data (optional — `steam_games_data.csv` is already included)

```bash
pip install requests
jupyter notebook Steam_Data_Collect.ipynb
```

> ⚠️ Collecting all 30,000 games takes ~13 hours due to the 1.6s delay per game. The script supports pause/resume — just re-run it and it will pick up where it left off.

### 2. Run the analysis

```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy
jupyter notebook Steam_Analysis_with_ML.ipynb
```

> **Note:** The CSV column is `Price_THB` — make sure any reference to `Price_USD` in the notebook is updated accordingly.

---

## Libraries Used

| Library | Purpose |
|---|---|
| `pandas` | Data loading, cleaning, grouping |
| `numpy` | Math operations, log transformation, residuals |
| `matplotlib` / `seaborn` | All visualizations |
| `scipy.stats` | pearsonr, spearmanr, pointbiserialr, f_oneway |
| `scikit-learn` | Random Forest, train/test split, cross-validation, metrics |
| `requests` | Steam API calls (data collection) |

---

| 8 | Platform Support vs Rating — Point-biserial r, ANOVA |
| 9 | Combined correlation heatmap (all factors) |
| 10 | Define success label & build feature matrix |
| 11 | Train Random Forest + evaluate (accuracy, ROC-AUC, CV) |
| 12 | Top 10 most popular games |
| 13 | Final summary: key findings |
| 14 | Save cleaned dataset |
