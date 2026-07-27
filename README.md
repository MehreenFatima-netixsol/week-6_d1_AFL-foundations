# AFL Data Foundations — EDA, Feature Engineering & Prediction Targets

**Week 6 · Day 1**

Building the analytical foundation for AFL match prediction and a domain-specific AFL AI assistant.

## Project Overview

This project performs an end-to-end exploratory data analysis (EDA) and feature engineering pipeline on historical Australian Football League (AFL) data. The objective is to prepare high-quality, leakage-free data for two downstream applications:

- Domain-Locked AFL Chat Assistant
- Machine Learning Models for predicting:
  - Match winners
  - Top-performing players
  - Leading goal kickers

The notebook emphasizes data understanding, target definition, reproducible preprocessing, and feature engineering following sports analytics best practices.

---

## Objectives

- Explore and understand the AFL datasets.
- Audit data quality and validate table relationships.
- Define prediction targets for teams and players.
- Perform exploratory data analysis (EDA).
- Engineer predictive features without data leakage.
- Build a reproducible time-based train/hold-out split.
- Generate a versioned feature table and feature dictionary.

---

## Dataset

The project uses four raw datasets.

| Dataset | Description | Grain |
|----------|-------------|-------|
| `team_matches_home_away_raw.csv` | Team match statistics | One Team–Match |
| `afl_players_round_by_round_stats_raw.csv` | Player match statistics | One Player–Match |
| `afl_players_seasonal_stats_raw.csv` | Seasonal player statistics | One Player–Season |
| `afl_players_info_raw.csv` | Player information | One Player |

The datasets are cleaned and consolidated into analytical tables using reusable ETL pipelines.

---

## Task 1 — Data Inventory & Understanding

Performed a complete audit of the datasets by:

- Loading all raw datasets
- Documenting table grain
- Identifying primary and foreign keys
- Validating joins using `match_id` and `player_id`
- Measuring historical coverage (seasons, teams, players)
- Detecting structural changes across AFL history
- Assessing data quality through:
  - Missing values
  - Duplicate records
  - Join integrity
  - Canonical team names
  - Impossible values and outliers

---

## Task 2 — Prediction Target Definition

### Match Winner

Two prediction targets were defined.

**Primary Target**

- Binary Classification
  - `home_win = 1`
  - `home_win = 0`

**Secondary Target**

- Winning Margin (Regression)

This allows both probability-based winner prediction and score margin estimation.

### Top Player

Three player-performance targets were defined.

- Top Disposal Getter
- Top Goal Kicker
- Match Impact Score (MIS)

MIS is a custom weighted metric combining offensive and defensive statistics and is validated against official AFL Fantasy Points.

---

## Task 3 — Exploratory Data Analysis

Key analyses include:

- Team win rates
- Home-ground advantage
- Season and ladder trends
- Player performance distributions
- Historical top performers
- Position-based comparisons
- Recent form vs. win probability
- Travel and rest-day effects
- Venue influence
- Correlation between engineered features

Multiple visualizations identify relationships useful for prediction.

---

## Task 4 — Feature Engineering

A leakage-free feature engineering pipeline was developed.

### Team Features

- Elo Ratings
- Win Streaks
- Rolling Win Rate
- Average Score
- Average Margin
- Ladder Position
- Ladder Percentage

### Player Features

- Rolling Goals
- Rolling Disposals
- Rolling Tackles
- Recent Match Output

### Context Features

- Days of Rest
- Venue
- Interstate Travel
- Head-to-Head Record
- Venue Win Rate

All rolling statistics are computed using **only previous matches**, preventing future information from leaking into the model.

---

## Task 5 — Train / Hold-Out Split

A reusable **time-based split** was implemented.

- Earlier seasons → Training
- Most recent season → Hold-Out Testing

A random split was intentionally avoided because it introduces future information and results in unrealistic model performance.

---

## Feature Dictionary

A feature dictionary accompanies the engineered dataset.

Each feature documents:

- Feature Name
- Description
- Source Columns
- Computation Window

This ensures reproducibility and consistency across future models.

---

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook


## Outputs

- Data Inventory Report
- Data Quality Assessment
- Prediction Target Definitions
- Exploratory Data Analysis
- Leakage-Free Feature Engineering
- Feature Dictionary
- Versioned Feature Table (CSV/Parquet)
- Time-Based Train/Test Split

---

## Key Learnings

- Understanding the dataset is essential before building predictive models.
- Clearly defined prediction targets improve model reliability.
- Time-series sports data requires strict prevention of data leakage.
- Feature engineering has a significant impact on model performance.
- Reproducible preprocessing pipelines ensure consistent model evaluation.

---

## Future Work

The engineered dataset produced in this project will be used for:

- AFL Match Winner Prediction
- Top Player Prediction
- Goal Kicker Prediction
- Model Evaluation and Comparison
- Domain-Specific AFL AI Chat Assistant

---

## Author

**Mehreen Fatima**
