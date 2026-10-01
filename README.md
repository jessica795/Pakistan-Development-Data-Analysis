# Pakistan Development Data Analysis

## Overview

This project examines long-term trends and statistical relationships among key economic, demographic, social, and environmental development indicators in Pakistan.

Using data from the **World Bank World Development Indicators (WDI)**, the project develops a reproducible statistical analysis workflow covering data collection, data quality assessment, exploratory data analysis, correlation analysis, regression modeling, and visualization.

The project focuses on identifying patterns and statistical associations within Pakistan's development indicators while considering important limitations such as missing observations, time trends, autocorrelation, multicollinearity, and differences in indicator availability.

---

## Research Question

> **How have key development indicators in Pakistan evolved over time, and what statistical relationships can be observed among economic, demographic, social, and environmental indicators?**

---

## Research Objectives

* Collect development indicators for Pakistan programmatically through the World Bank API.
* Organize and validate the collected data.
* Assess missing observations and potential data-quality issues.
* Examine long-term trends in selected development indicators.
* Explore relationships among economic, demographic, social, and environmental indicators.
* Apply Pearson correlation analysis.
* Apply simple and multiple Ordinary Least Squares (OLS) regression.
* Visualize major development trends and statistical relationships.
* Document methodological limitations and considerations for interpretation.
* Maintain a reproducible and organized research workflow.

---

## Research Highlights

* **66 annual observations** covering **1960–2025**.
* **10 development indicators** collected from the World Bank.
* Programmatic data collection through the **World Bank API**.
* Exploratory analysis of economic, demographic, social, and environmental trends.
* Pearson correlation analysis between selected development indicators.
* Simple and multiple OLS regression models.
* Reusable Python functions for data cleaning, statistical analysis, and visualization.
* Explicit consideration of missing data, autocorrelation, multicollinearity, and time-trend effects.

---

## Data Source

**Primary Source:** World Bank — World Development Indicators (WDI)

The data were collected programmatically using the World Bank API.

**Country:** Pakistan
**Observation period:** 1960–2025
**Frequency:** Annual
**Number of indicators:** 10

The raw dataset is preserved separately from the processed dataset to support transparency and reproducibility.

---

## Indicators

| Indicator             | Description                                          |
| --------------------- | ---------------------------------------------------- |
| GDP Growth            | Annual percentage growth of GDP                      |
| GDP per Capita        | GDP per capita in current US dollars                 |
| Inflation             | Consumer price inflation                             |
| Unemployment          | Unemployment rate                                    |
| Population            | Total population                                     |
| Population Growth     | Annual population growth                             |
| Urban Population      | Urban population as a percentage of total population |
| Life Expectancy       | Life expectancy at birth                             |
| Access to Electricity | Percentage of population with access to electricity  |
| Renewable Energy      | Renewable energy consumption indicator               |

---

## Methodology

### 1. Data Collection

Development indicators were retrieved from the World Bank API using Python.

The API-based approach allows the dataset to be collected systematically rather than manually, improving reproducibility and reducing the risk of transcription errors.

The original downloaded dataset is stored in:

```text
data/raw/
```

---

### 2. Data Cleaning

The data-cleaning workflow includes:

* Checking data types
* Converting year values to numeric format
* Sorting observations chronologically
* Checking duplicate observations
* Identifying missing values
* Preparing variables for statistical analysis
* Creating a processed dataset for subsequent analysis

Missing observations were retained rather than being replaced indiscriminately.

This is particularly important because several indicators are not available for the complete 1960–2025 period.

The processed dataset is stored in:

```text
data/processed/
```

---

### 3. Exploratory Data Analysis

Exploratory analysis was conducted to examine the historical development of selected indicators in Pakistan.

The analysis includes visualizations of:

* GDP growth
* GDP per capita
* Population
* Population growth
* Life expectancy
* Urban population
* Access to electricity
* Renewable energy

A correlation matrix was also generated to explore statistical relationships among the numerical variables.

---

### 4. Statistical Analysis

The project applies:

* **Pearson correlation**
* **Simple Ordinary Least Squares (OLS) regression**
* **Multiple Ordinary Least Squares (OLS) regression**

The primary regression analysis examines the relationship between:

**GDP per capita → Life expectancy**

A multiple regression model examines life expectancy using:

* GDP per capita
* Urban population
* Access to electricity

The statistical analysis was implemented using **SciPy** and **Statsmodels**.

---

# Key Findings

## GDP per Capita and Life Expectancy

The Pearson correlation between GDP per capita and life expectancy was:

**r = 0.851**

with:

**p < 0.001**

based on **65 available observations**.

This indicates a strong positive statistical association between the two variables within the observed dataset.

A simple OLS regression produced:

**R² = 0.724**

The GDP-per-capita coefficient was statistically significant at conventional significance levels.

However, this relationship should be interpreted as an **association rather than evidence of a causal effect**.

---

## Multiple Regression

A multiple OLS model was estimated using:

* GDP per capita
* Urban population
* Access to electricity

as predictors of life expectancy.

The model produced:

**R² = 0.967**

and was estimated using:

**n = 27 observations**

The reduced sample size results from the limited availability of electricity-access observations over the full study period.

Within this model:

* GDP per capita showed a statistically significant positive association with life expectancy.
* Urban population showed a statistically significant positive association with life expectancy.
* Access to electricity was not statistically significant at conventional significance levels.

These results describe statistical relationships within the available sample and should not be interpreted as causal estimates.

---

# Statistical Considerations

## Time Trends

Several development indicators show strong correlations with Year.

For example, the dataset shows strong positive correlations between Year and variables such as population, urban population, life expectancy, and access to electricity.

Such relationships can partly reflect common long-term development trends.

Therefore, a high correlation between two variables does not necessarily imply that one variable causes changes in the other.

---

## Autocorrelation

The simple GDP-per-capita regression produced a Durbin-Watson statistic of approximately:

**0.12**

This indicates substantial positive residual autocorrelation.

Because observations are annual time-series data, conventional OLS assumptions regarding independent errors may not hold.

Consequently, the regression results should be interpreted cautiously rather than treated as definitive causal evidence.

---

## Multicollinearity

The multiple regression model produced a high R², but the predictor variables are themselves strongly related to long-term development trends.

The model also showed a high condition number, indicating potential multicollinearity and numerical instability among predictors.

Therefore, individual regression coefficients should be interpreted with caution.

---

# Data Quality

The combined dataset contains:

* **66 observations**
* **10 development indicators**
* **1960–2025 observation period**

Missing observations vary considerably by indicator.

Some variables have near-complete coverage, while others have substantial gaps.

For example, unemployment, access to electricity, and renewable-energy-related observations have more limited historical availability than population or GDP-per-capita data.

Rather than artificially filling missing observations, the project preserves the missing values and allows individual statistical analyses to use the available observations for the variables involved.

---

# Visualizations

The project includes visualizations examining long-term development trends and relationships among indicators.

Examples include:

* GDP per capita over time
* GDP growth over time
* Population over time
* Life expectancy over time
* Urban population over time
* Access to electricity over time
* Renewable energy trends
* Development-indicator correlation heatmap
* Relationships between selected development indicators

Generated figures are stored in:

```text
figures/
```

---

# Repository Structure

```text
Pakistan-Development-Data-Analysis/
│
├── README.md
├── requirements.txt
├── LICENSE
│
├── data/
│   ├── raw/
│   │   └── pakistan_development_raw.csv
│   │
│   └── processed/
│       └── pakistan_development_processed.csv
│
├── notebooks/
│   ├── 01_data_collection.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_exploratory_analysis.ipynb
│   ├── 04_statistical_analysis.ipynb
│   └── 05_findings_and_visualization.ipynb
│
├── figures/
│
├── results/
│   ├── descriptive_statistics.csv
│   └── regression_results.txt
│
└── src/
    ├── data_cleaning.py
    ├── analysis.py
    └── visualization.py
```

---

# Tools & Technologies

### Programming

* Python

### Data Analysis

* Pandas
* NumPy

### Statistical Analysis

* SciPy
* Statsmodels

### Visualization

* Matplotlib
* Seaborn

### Data Collection

* World Bank API
* Requests

### Research & Reproducibility

* Google Colab
* GitHub

---

# Reproducibility

The project follows the workflow:

```text
World Bank API
      ↓
Raw Data
      ↓
Data Cleaning
      ↓
Processed Data
      ↓
Exploratory Data Analysis
      ↓
Statistical Analysis
      ↓
Findings & Visualization
```

Reusable functions for data preparation, statistical analysis, and visualization are available in the `src/` directory.

Python dependencies required for the project are listed in:

```text
requirements.txt
```

The raw dataset is retained separately from the processed dataset so that the transformation and analysis workflow can be examined independently.

---

# Limitations

This project is intended as an **exploratory statistical analysis** rather than a causal study.

Important limitations include:

* Missing observations for several indicators.
* Unequal data availability across indicators.
* Strong long-term time trends among several variables.
* Potential autocorrelation in regression residuals.
* Potential multicollinearity among predictors.
* Reduced sample size in the multiple regression model.
* Conventional OLS inference may not fully account for time-series characteristics.
* Correlation and regression results do not establish causal relationships.

Future extensions could incorporate time-series-specific methods, additional socioeconomic indicators, robustness checks, and alternative modeling approaches.

---

# Author

**Jassica Michael**

**BS Statistics — Quaid-i-Azam University**

Research interests:

* Statistical Analysis
* Data Science
* Machine Learning
* Time Series Analysis
* Development Data
* Evidence-Based Research
* Monitoring & Evaluation

GitHub: `https://github.com/jessica795`

---

## Project Purpose

This project was developed to demonstrate practical application of statistical methods to real-world development data, with an emphasis on **data quality, reproducibility, statistical reasoning, and responsible interpretation of results**.
