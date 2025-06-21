# rainfall-prediction

# Project 
1. Objective:
The goal was to build a first‑pass model that can guess how much rain will fall in Austin on a given day from the other weather readings already reported by the local weather station. Because I only wanted a quick numerical baseline, I chose ordinary least‑squares linear regression—fast, interpretable, and easy to compare against more sophisticated models later. 

# 2. Methodology
Data scope – Daily records for roughly 800 days (2013‑2017) with nine original columns such as temperature, humidity, wind, visibility, and the target Precipitation Sum (Inches).

Cleaning steps
- Dropped three columns that were either textual (Events, Date) or redundant (SeaLevelPressureLowInches).

- Replaced the symbols “T” (trace rainfall) and “–” (missing) with 0.0 so every column is purely numeric.

- Saved the tidy frame as austin_weather_final.csv so the notebook can reload a clean copy at any time.

Feature / target split – Predictors: TempAvgF, DewPointAvgF, HumidityAvgPercent, SeaLevelPressureAvgInches, VisibilityAvgMiles, WindAvgMPH (6 in total). 
Target: PrecipitationSumInches, reshaped to (n, 1) for scikit‑learn.

# 3. Analysis process
- Time‑series scatter: showed a heavily right‑skewed pattern—>80 % of days have no rain; a few extreme days top ~4 in.

- Pairwise plots: strongest positive trends with rainfall were humidity (>70 %) and dew‑point (>65 °F). Temperature had a mild negative slope; pressure, visibility, and wind were nearly flat.

- Collinearity check: all pairwise |r| < 0.55, so no variable had to be removed for multicollinearity.

# 4. How I built and checked the model
- Trained LinearRegression() on the full feature matrix (no regularisation).

- Highlighted day #798 in every plot to show how the model behaves on an extreme‑rain day.

- Quick 80 / 20 train‑test split for sanity: R² ≈ 0.22, RMSE ≈ 0.32 inches. That means the linear model explains about one‑fifth of the variability—acceptable as a starting point but clearly improvable with non‑linear methods.

# 5. Key findings
- With increase in temperature and humidity the chances of rainfall increases(inference from precipiation size) 

- Dry days dominate: most Austin days record 0 in of precipitation; when rain does come, it can be intense.

- Humidity & dew‑point matter most: every extra 10 % in average humidity adds ~0.05 in to expected rainfall, holding other factors constant.
