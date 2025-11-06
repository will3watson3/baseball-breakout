# MLB Breakout Player Prediction/Analysis

## Overview
This project analyzes Statcast data to identify which underlying hitting metrics — like hard-hit rate, barrel rate, and contact quality — best predict MLB breakout seasons. Using year-over-year improvements (deltas) in player process metrics, it builds a machine learning model that forecasts which hitters are most likely to “break out” in the upcoming season.

** Project Goals ** 

1. Predict which MLB hitters are most likely to “break out” in an upcoming season based on improvements in underlying skill-based metrics rather than traditional statistics.
2. Identify which process-driven features (such as hard-hit rate, barrel rate, walk rate, and contact consistency) are the strongest predictors of future breakout performance.
3. Establish interpretable thresholds for those key features — i.e., the level of improvement in metrics like barrel rate or hard-hit % that meaningfully increases a player’s breakout probability.
4. Build a transparent machine learning model (using XGBoost and SHAP) that not only predicts breakouts accurately but also explains why each player’s projection is high or low.
5. Deliver actionable insights for analysts and front offices, highlighting which players’ process improvements indicate true skill growth versus statistical noise.


## Methodology

1. Data Collection:
- Collected Statcast data for all qualified hitters from 2022-2025
- Integrated year over year changes of stats (deltas) to encapsulate how much each underlying stat went up or down

2. Breakout Player Labeling:
- Players were labeled as breakouts or non-breakouts based on past year over year statistic deltas
- Only players with over 200 plate appearances were considered to ensure a large enough sample size and not skew the results
- Players were only flagged as breakouts if they showed significant increases in overall hitting output supported by underlying skill growth metrics
- All players were put into a data set with a column labeling them as breakout player (1) or a non-breakout player (0) and this helps fuel later stages of the model

3. Machine Learning Model Training:
- 2 machine learning models were trained to identify breakouts from the dataset created in the breakout player labeling stage: The models used are XGboost Classifier and Logistic Regression
- XGboost serves as the primary model due to its strong performance and accuracy with Logistic Regression was used as a baseline comparison
- The models were trained on 2022-2024 data and tested on 2025 data
- The models were also analyzed based on which factors were driving their decisions most heavily 

4. Prediction & Explainability:
-  The final stage was using the Machine learning model that was built to predict breakout players for next year (2026)
-  Each prediction included a breakout probability score and a model driven explanation as to why the model thinks a certain player will breakout
-  The results were exported as ranked predictions with interpretable insights for scouting and analytical evaluation


## Results and Key Insights
- The XGBoost model achieved exceptional predictive accuracy on the 2025 validation set (ROC AUC ≈ 0.99, Avg. Precision ≈ 0.96), outperforming the logistic regression baseline.
- Model interpretability revealed that contact quality (barrel rate, hard-hit%), plate discipline improvements (BB/K ratio), and launch characteristics (attack angle, launch speed) were the most influential factors in predicting breakouts.
- Several 2026 hitters — including Addison Barger, Alejandro Kirk, and Gavin Sheets — surfaced as high-probability breakout candidates, driven by measurable gains in approach and contact metrics.
- The project provides a data-driven framework for identifying emerging offensive talent, with applications in player development, fantasy projections, and front-office scouting.

## Limitations and Future Areas of Exploration
- The model currently depends heavily on process score(a combination of all statistical year over year stat changes) and plate appearance deltas, which may overrepresent playing time or opportunity rather than pure skill growth.
- Breakout Labels were only given to players with past experience in the MLB this excludes players who broke out in their rookie season which is often times when many breakout seasons happen
- Statcast has great metrics and more usable metrics than anyone else however a lot of their more in depth stats are not downloadable, so in order to access them it would take a lot of web scraping.
- For many players a breakout could happen seemingly out of nowhere based on a change made in the offseason, something a coach said that stuck or confidence derived from a few good outcomes, which can be hard to detect using just result based statistics.
- Future work will include:
  1. Integrating minor league data for better in depth analysis
  2. Refining the algorithm that determines the label of a "Breakout Player"
  3. Expanding the model to include multiple years leading up to a breakout for a single player to capture players that slowly improve their skills quietly until they finally have a breakout season
  4. Expand the statistics used to determine breakout by getting more in depth stats such as stats about vs. certain pitches, pitchers or in game situational stats such as with bases loaded.

## Tech Stack
- Data Source: Statcast (Baseball Savant)
- Environment: Jupyter Notebook
- Language: Python
- Core Libraries:
1. Pandas
2. Numpy
3. Scikit-learn
4. XGboost
5. Shap
6. Joblib
7. Matplotlib / Seaborn
8. Pathlib / OS







  