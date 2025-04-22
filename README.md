# Premier League xG Prediction Model

This project follows a structured pipeline to build an expected goals (xG) predictive model using Premier League data:

## 1. 🔎 Web Scraping Shot-Level Data
We scraped detailed shot-level data for the 2023/24 Premier League season directly from Understat, using a Python-based script.

This data includes:
- Player name
- Team
- xG value
- Shot type
- Match minute
- Match date
- Home/Away status
- And more

## 2. 📊 Constructing Match-Level Data
Shot-level records were aggregated into match-level metrics for each team and match.

**Features created include:**
- `total_xG`: sum of xG values
- `shot_count`: total number of shots
- `avg_shot_xG`: average quality per shot
- `goals`: actual goals scored

## 3. 🏟️ Generating Home & Away Form Summaries
Rolling metrics were computed separately for home and away matches over each team’s last 5 fixtures.

**These summaries include both attacking and defensive rolling metrics:**

- **Offensive:** `rolling_xG`, `rolling_shots`, `rolling_avg_shot_xG`, `rolling_conversion_rate`
- **Defensive:** `rolling_shots_conceded`, `rolling_goals_conceded`, `rolling_opponent_conversion_rate`

## 4. 🔁 Combining Features into a Training Dataset
The `Home_Form_Summary` and `Away_Form_Summary` files were merged based on match IDs to create the `Match_Training_Dataset.csv`.

This dataset contains one row per match, with rolling metrics for both teams heading into the match.

## 5. 🤖 Model Training & Evaluation
A machine learning regression model (Gradient Boosting Regressor) was trained using:

- **Input features:** team form metrics (offensive + defensive)
- **Target variables:** home goals and away goals

The model's performance was evaluated using:
- **Mean Absolute Error (MAE)**
- **Root Mean Squared Error (RMSE)**
