# Flight Data Analysis and Prediction

# Table of Contents
1. [Introduction](#introduction)
2. [Dataset Description](#dataset-description)
3. [Overview](#overview)
4. [Dependencies](#dependencies)
5. [Usage](#usage)
6. [Files Included](#files-included)
7. [Analyses](#analyses)
   - [Summary of Training Data](#summary-of-training-data)
   - [Histograms](#histograms)
   - [Correlation Matrix](#correlation-matrix)
   - [Modeling Results](#modeling-results)

## Introduction
This repository contains Python code for analyzing flight data and predicting Take-Off Weight (TOW) using regression techniques. The repository includes data preprocessing, exploratory data analysis (EDA), feature engineering, model building (Linear Regression and Random Forest), hyperparameter tuning using Grid Search, and prediction of TOW for validation data.

## Dataset Description
The dataset consists of flight data including various numerical attributes such as ActualFlightTime, ActualTotalFuel, FLownPassengers, BagsCount, and FlightBagsWeight. These attributes are used to predict the Actual Take-Off Weight (ActualTOW) of flights.

## Overview
The script performs the following tasks:

1. **Data Loading and Cleaning:** Loads training and validation datasets from CSV files, inspects basic information (e.g., data types, missing values), and replaces missing values with median values.

2. **Data Transformation:** Converts selected columns to numeric values where applicable and applies normalization to numerical features using StandardScaler from scikit-learn.

3. **Exploratory Data Analysis:** Visualizes data distributions using histograms. Explores correlations between variables using a heatmap.

4. **Outlier Removal:** Implements a function to detect and remove outliers based on the Interquartile Range (IQR) method for selected numerical columns.

5. **Modeling:** Constructs a Linear Regression model to predict Take-Off Weight (TOW) based on fuel consumption, flown passengers, and baggage weight. Develops a Random Forest Regressor model and performs hyperparameter tuning using Grid Search. Evaluates model performance using Root Mean Squared Error (RMSE) metric on a test set.

6. **Prediction:** Applies the best performing Random Forest model to predict TOW for a validation dataset and saves predictions to a CSV file.

## Dependencies
- Python 3.x
- Required Python packages (`pandas`, `numpy`, `seaborn`, `matplotlib`, `scikit-learn` )

## Usage
To run the analysis, ensure you have Python installed along with the required libraries listed above. Adjust the paths to your CSV files (`training.csv` and `validation.csv`) accordingly in the script, then execute the script. The results including visualizations and model evaluations will be displayed in the console and/or saved to files as specified.

## Files Included
`flight_data_analysis.py`: Python script containing the complete data analysis pipeline.

`validation_predictions.csv`: CSV file containing predicted TOW values for the validation dataset.

## Analyses

### Summary of Training Data
**Data Consistency:**
Columns DepartureYear, DepartureMonth, and DepartureDay are consistent, indicating data collected over a specific period (October 1-15, 2016).

**Potential Outliers:**
Average actual flight time is about 110 minutes with a standard deviation of approximately 50.7 minutes. Flight times range from 2 to 1504 minutes, suggesting potential outliers or exceptional cases.

**Data Standardization:**
Columns ActualTotalFuel, FlownPassengers, and FlightBagsWeight have been standardized (mean close to 0 and standard deviation close to 1), facilitating comparison between their distributions and values.

- ActualTotalFuel: Values range from -2.08 to 6.69, indicating significant variability in fuel consumption.

- FlownPassengers: Passenger counts range from -2.97 to 1.68, suggesting diversity in the number of passengers carried.

- BagsCount: Average bags per flight is around 44 with a standard deviation of approximately 23.8. The count ranges from 1 to 116, showing variability in baggage quantity.

- FlightBagsWeight: Bag weight ranges from -1.82 to 2.74.

**ActualTOW (Take-Off Weight):** Average take-off weight is about 65,437 kg with a standard deviation of approximately 2550 kg. Take-off weights range from 57,794 kg to 73,122 kg, indicating a reasonable distribution of weights in the data.

### Histograms

![rozkład zmiennych train](https://github.com/agnieszkacieciwa/Flight-Data-Analysis-and-Prediction/assets/88035266/90483439-7213-49e4-b3db-2d84cb409b00)

- **DepartureYear:** Data spans only one year (2016), suggesting consistency throughout the dataset.
- **DepartureMonth:** All flights occurred in October, indicating uniformity in departure month.
- **DepartureDay:** Departure days are evenly distributed over the first 15 days of the month, suggesting evenly distributed flights during this period.
- **FlightNumber:** Flight numbers appear evenly distributed, with some values occurring more frequently.
- **ActualFlightTime:** Actual flight times have a distribution where most flights are short (peak within the first 250 minutes), but there are also a few long flights (up to 1500 minutes).
- **ActualTotalFuel:** Most flights consume smaller amounts of fuel (majority below 5000 units), but there are also flights consuming significantly more fuel.
- **ActualTOW (Take-Off Weight):** Take-off weights have a normal distribution, with most flights having weights between 60,000 and 70,000 units.
- **FlownPassengers:** Most flights carry fewer passengers, with a peak around 100 passengers. Some flights carry more passengers.
- **BagsCount:** Bag counts per flight have a distribution where most flights carry fewer bags (peak below 100 bags), but there are flights with more bags.
- **FlightBagsWeight:** Bag weights per flight show a similar distribution to bag counts, with most flights having lighter bags, but some flights have heavier bags.

### Correlation Matrix

![correlation](https://github.com/agnieszkacieciwa/Flight-Data-Analysis-and-Prediction/assets/88035266/ee8ac382-5969-431f-a51d-e50ab0ec25b0)


Strong positive correlations between ActualFlightTime, ActualTotalFuel, and ActualTOW indicate their interrelationships.
FlownPassengers, BagsCount, and FlightBagsWeight also show some positive correlations.


DepartureDay, FlightNumber, DepartureYear, and DepartureMonth have no significant correlations with other variables.

### Modeling Results

RMSE for Linear Regression: 1015.0364494658272

RMSE for Random Forest Model: 1080.7306918837298

Best RMSE after Grid Search for Random Forest: 1007.5614302349079


**The best RMSE was achieved with the Random Forest model, with an average prediction error of approximately 1008 kg in predicting aircraft take-off weight.**

