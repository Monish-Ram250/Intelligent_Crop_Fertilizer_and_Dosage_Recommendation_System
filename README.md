# Intelligent Crop Fertilizer and Dosage Recommendation System

## Project Overview

This project is an intelligent agricultural recommendation system that predicts the most suitable crop, recommends a fertilizer, and estimates the required dosage based on soil nutrients and climatic conditions.

The main goal of the project is to support data-driven farming decisions, reduce fertilizer misuse, improve productivity, and promote sustainable agriculture.

## What This Project Does

- Recommends a suitable crop based on soil and climate inputs
- Predicts a primary fertilizer recommendation
- Estimates fertilizer dosage per hectare
- Calculates total dosage based on land size
- Helps farmers make better agricultural decisions using machine learning

## Dataset Information

The dataset used in this project was collected from multiple sources, including Kaggle and government agricultural repositories. These datasets were cleaned, combined, and merged into a single unified dataset for model training and prediction.

## Dataset Features

The merged dataset includes agricultural and environmental features such as:

- N, P, K
- pH
- OC, S, Zn, Fe, Cu, Mn, B
- Temperature
- Humidity
- Rainfall

It also contains crop labels, fertilizer-related information, and dosage-related values used for prediction.

## Data Preprocessing

The preprocessing steps used in this project include:

- Removing duplicate records
- Verifying valid data types and ranges
- Selecting relevant numeric features
- Filling missing values in feature columns using median values
- Encoding crop and fertilizer labels
- Avoiding data leakage by excluding direct target-related columns from input features

## Model Architecture

This project uses a multi-model machine learning pipeline built with XGBoost:

- XGBoost Classifier for crop recommendation
- XGBoost Classifier for fertilizer recommendation
- XGBoost Regressor for dosage prediction

The models are trained and optimized using RandomizedSearchCV with cross-validation.

## Workflow

1. Collect and merge agricultural datasets from Kaggle and government sources
2. Clean and preprocess the merged dataset
3. Select useful soil and climate features
4. Train a crop recommendation model
5. Train a fertilizer recommendation model
6. Train a dosage prediction model
7. Accept user input for soil and environmental values
8. Predict crop, fertilizer, dosage per hectare, and total dosage based on land area

## Evaluation Metrics

The project uses different evaluation metrics for classification and regression tasks:

### For Crop and Fertilizer Prediction
- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix

### For Dosage Prediction
- MAE
- RMSE
- R² Score

## Output

For a given set of soil and climate values, the system provides:

- Predicted crop
- Predicted fertilizer
- Predicted combined dosage per hectare
- Total dosage required based on land size

## Visualizations

The notebook also includes visualization components such as:

- Nutrient and climate radar chart
- Dosage distribution chart

These visualizations help compare user input with dataset trends and make the recommendations easier to understand.

## Tech Stack

- Python
- Pandas
- NumPy
- Scikit-learn
- XGBoost
- Matplotlib
- Seaborn

## Real-World Impact

This project can help in:

- Improving crop planning
- Reducing excessive fertilizer usage
- Supporting precision agriculture
- Making farming recommendations more data-driven
- Encouraging sustainable agricultural practices

## Limitations

- The dataset is based on static historical data
- It may include regional bias
- It does not currently use real-time weather APIs
- It should be used as a decision-support tool, not as a replacement for expert agricultural advice

## Future Scope

- Integration with real-time weather APIs
- Region-specific fertilizer recommendation rules
- Web or mobile application deployment
- Integration with IoT or satellite-based soil monitoring systems

## Author

Akula Monish Ram
B.Tech CSE
