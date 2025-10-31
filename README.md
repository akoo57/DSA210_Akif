# NBA Regular Season Success Analysis: Financial Strategies and Roster Engineering

## Project Overview

This serves as the final project for the Data Science Analysis (DSA) course. Its primary objective is to analyze the key factors influencing the **regular season** success of NBA teams. This project deviates from focusing purely on on-court statistics to instead concentrate on "front office" decisions.

Under the constraints of a rigid Salary Cap, this analysis will statistically examine how teams allocate their financial resources (e.g., investment in superstars, luxury tax payments), manage roster stability (e.g., player continuity), and how roster demographics (e.g., age, experience) impact overall performance. The goal is to determine which roster engineering and financial strategies exhibit the strongest predictive power on regular season `Win_Percentage` and efficiency (`Net_Rating`).

## Project Objectives

1.  **To Analyze the Impact of Financial Strategies**
    * To examine the effect of salary concentration among superstars (`Top3_Salary_Share`) and the payment of the `Luxury_Tax` on regular season success.

2.  **To Quantify the Role of Roster Engineering**
    * To investigate the relationship between roster stability (`Minutes_Continuity`) and the team's weighted average age (`Avg_Age_Weighted`) with team efficiency (`Net_Rating`) and defensive prowess (`Defensive_Rating`).

3.  **To Model Financial Inefficiency**
    * To quantitatively determine the negative impact of "dead money" (`Dead_Money_Share`)—salaries paid to players no longer on the roster—on the total `Win_Percentage`.

4.  **To Identify Key Success Factors**
    * To utilize multivariate linear regression models to identify which strategic variables serve as the most statistically significant predictors of regular season success.

5.  **To Apply Data Science Methodologies**
    * To apply skills learned in this course—including web scraping, data cleaning, exploratory data analysis (EDA), hypothesis testing, and regression modeling—to a real-world dataset.

## Motivation

This project merges a personal passion for basketball with a professional interest in data science. The NBA, with its strict salary cap regulations, provides a perfect "laboratory" environment for data-driven strategic analysis.

* **Strategic Analysis:** I aim to move beyond the simple question of "Does money buy success?" Is paying the luxury tax a prerequisite for contention, or is it often a sign of inefficient resource allocation?
* **Roster Engineering:** Is sustainable success built through major annual trades, or by retaining a core roster to develop team "chemistry" (`Minutes_Continuity`)?
* **Superstars vs. Depth:** Is it more efficient to allocate 70% of the salary cap to three superstars (`Top3_Salary_Share`), or to build a balanced roster with 8-9 quality contributors?
* **The Experience Factor:** I want to quantify the precise impact of "veteran experience" on defensive performance (`Defensive_Rating`).

The prospect of answering these questions using empirical data is the core motivation for this project.

## Dataset

This project will utilize **panel data** covering all 30 NBA teams over a 10-season span (e.g., 2014-2024). The data will be collected and merged from the following sources.

### **Team Performance Data**
* **Win Percentage (Regular Season)**
* **Net Rating** (Point differential per 100 possessions)
* **Defensive Rating** (Points allowed per 100 possessions)

### **Financial & Roster Data**
* **Team Payroll & Luxury Tax Status**: Total team salary and tax payment status.
* **Top 3 Player Salary Share**: Percentage of the Salary Cap consumed by the team's three highest-paid players.
* **Dead Money Share**: Percentage of the Salary Cap allocated to players no longer on the roster.
* **Minutes Continuity**: Percentage of minutes played by returning players from the previous season.
* **Weighted Average Age**: Team's average age, weighted by minutes played.

### **Data Sources**
* **Financial Data (Salary, Tax, Dead Money):** `Spotrac.com`
* **Team & Player Statistics (Wins, Ratings, Age, Minutes):** `Basketball-Reference.com`
The final dataset will be structured with a unique key for `(Team, Season)`.

## Tools and Technologies

* **Python** → Primary language for data processing, analysis, and modeling.
* **Pandas** → For data manipulation, cleaning, and merging.
* **Requests & BeautifulSoup4** → For web scraping data from `Spotrac` and `Basketball-Reference`.
* **Matplotlib & Seaborn** → For data visualization and exploratory data analysis.
* **Scikit-learn** → For machine learning models (specifically `LinearRegression`).
* **SciPy & Statsmodels** → For hypothesis testing, correlation analysis, and checking for multicollinearity (VIF).

## Analysis Plan

### Data Collection and Preprocessing
* Scrape financial and statistical data for the relevant seasons using Python libraries.
* Merge the datasets from the two sources into a unified `pandas` DataFrame using `(Team, Season)` as the primary key.
* Handle missing values and standardize all financial fields, either against the annual Salary Cap (as a percentage) or by adjusting for inflation.

### Exploratory Data Analysis (EDA) and Visualization
* Generate a correlation heatmap using `seaborn` to identify initial relationships and potential multicollinearity between predictors.
* Create a scatter plot to visualize the relationship between `Top3_Salary_Share` and `Win_Percentage`.
* Utilize box plots to compare the `Net_Rating` distributions for `Luxury_Tax_Status` groups (1 vs. 0).

### Statistical Modeling and Hypothesis Testing
* Formally test the five core hypotheses (see below).
* Construct a **Multivariate Linear Regression Model**:
    * `Win_Percentage ~ β₀ + β₁(Top3_Share) + β₂(Avg_Age) + β₃(Continuity) + β₄(Dead_Money) + β₅(Luxury_Tax) + ε`
* Evaluate the model's overall significance (F-test) and the statistical significance of individual coefficients (β) using p-values to accept or reject the hypotheses.
* Assess and mitigate multicollinearity by examining Variance Inflation Factor (VIF) scores for all predictors.

## Core Hypotheses

The project will formally like:

* **Hypothesis 1 (The "Superstar" Strategy):**
    * **$H_0$**: There is no statistically significant relationship between a team's `Top3_Salary_Share` and its `Win_Percentage`.
    * **$H_1$**: There is a statistically significant positive relationship between `Top3_Salary_Share` and `Win_Percentage`.

* **Hypothesis 2 (The Price of Contention):**
    * **$H_0$**: There is no statistically significant difference in the average `Net_Rating` between teams that pay the luxury tax and teams that do not.
    * **$H_1$**: Teams with `Luxury_Tax_Status = 1` have a statistically significant higher average `Net_Rating` than teams with `Luxury_Tax_Status = 0`.

* **Hypothesis 3 (The "Chemistry" Factor):**
    * **$H_0$**: There is no statistically significant relationship between a team's `Minutes_Continuity` and its `Net_Rating`.
    * **$H_1$**: There is a statistically significant positive relationship between `Minutes_Continuity` and `Net_Rating`.

* **Hypothesis 4 (Experience and Defense):**
    * **$H_0$**: There is no statistically significant relationship between a team's `Avg_Age_Weighted` and its `Defensive_Rating`.
    * **$H_1$**: There is a statistically significant negative relationship between `Avg_Age_Weighted` and `Defensive_Rating` (i.e., as age increases, points allowed *decrease*).

* **Hypothesis 5 (The "Dead Money" Drag):**
    * **$H_0$**: There is no statistically significant relationship between a team's `Dead_Money_Share` and its `Win_Percentage`.
    * **$H_1$**: There is a statistically significant negative relationship between `Dead_Money_Share` and `Win_Percentage`.

## Expected Outcomes

By the conclusion of this project, I expect to provide data-driven answers to the following questions:

* Is paying the luxury tax a statistically significant predictor of regular season success, or merely a byproduct of it?
* Which strategy yields a higher return in wins: concentrating salary in 2-3 superstars or distributing it across a deeper, more balanced roster?
* What is the quantitative impact of "roster chemistry," as measured by `Minutes_Continuity`, on a team's overall efficiency?
* What is the "cost" of bad contracts, measured in terms of `Win_Percentage` lost per percentage point of the cap dedicated to `Dead_Money`?
* Do veteran teams (higher `Avg_Age_Weighted`) demonstrate empirically superior defensive performance?
