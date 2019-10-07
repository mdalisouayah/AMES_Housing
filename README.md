# Ames Housing Pricing Model

## Introduction

The objective of this project is to create a regression model based on the Ames Housing Dataset.

The Ames Housing Dataset is comprised of two csv files: a training set with features and  sale prices, and a test set with just the features. The prediction of the prices pertaining to the test dataset are the subject of the Kaggle competition. The RMSE is the metric chosen to evaluate the model's strength.  

Several versions of the model have been submitted to the Kaggle competion. the best scoring model will be the main subject of analysis in this technical report. However, unsuccessful attempts to improve the model will be described, when relevant, as they tried to address a particular Data science issue.

## The Data Science problem and process

The objective of this exercise is to put the data in a clean, interpretable, and malliable format and build a pricing model that would help estimate home prices based on selected features.
The model is designed to be a useful tool for a number of stakeholders, including city government, real estate agents and home buyers and sellers.

## Scope of the Project

**The outline below covers the scope of the steps taken in this modeling exercise:**
  - a high-level exploration of the data, using `summary statistics`
  - identification of missing data, using the `.info` function
  - exploring options to impute data using `value_counts` and the information provided in the `data dictionary`
  - study of `correlations`, using correlation matrix and `Heatmaps`
  - selection of features, based on a correlation threshold, and when appropriate dropping features based on `multicollinearity`
  - dummying categorical variables, using pandas built-in function
  - `feature engineering`, using `PolynomialFeatures`


## Data cleaning

**Identification of missing or inconsistent values**
The training dataframe has almost 80 features and about 2500 records of sale transactions. The information shows a number of missing values. We know at this point that further investigation is needed to make a decision about the missing data.
A preliminary statistical analysis shows no obvious discrepancy or typos in the numerical data, such as negative prices, areas, or number of rooms, etc. The `.describe()` with a focus on `Min` and `Max` was used as the main tool for this.  

**2 main tools have been used to make educated guesses about the missing data:**
1. _the data dictionary_: it allowed to explore the different options that a value can take.
2. _the value_counts()_ function: allowed to explore the distribution of the values.

**Data imputation and creation of function**
In some cases a decision was taken to mark the missing values as NA (for none applicable) or None, when such an option is provided for in the data dictionary, but not used as an entry option. In other cases the distribution of the existing values was relied upon to assign a value to the missing data. The imputation varied between, means or modes for numerical continuous data, and the middle, or the most used option for categorical and discrete values. The logic here is that if a mistake in judgement takes places, the worst that could happen would just tilt the values more toward the mean values. Finally, functions were defined to reproduce the above transformations to similar cases within the training set as well as the test data.

### Exploratory visualization: heatmaps, correlation and multi-collinear matrices
As a first step to understanding the data a correlation matrix, coupled with a heatmap of correlations, has been drawn.
It was obvious that only a dozen of features had a relatively strong correlation (threshold >=50%) with the `saleprices`. However, it was decided that for the first model all features will be used. Later, based on the model evaluation, a more rigorous approach to feature selection will be taken. This is known as the backward approach to feature selection.
Along this process, all categorical features have been `dummified` to allow their modeling. At this stage, the `dataframe` was over 300 feature large.

### Model choice
When plotted against continuous features, `saleprices` rather approximated a linear distribution, thus the linear regression model was chosen as the base model. Later, the choice was confirmed given the quasi-normal distribution of the residuals.

#### train-test split, scaling, and cross-validation
The data was split between train and test data. The purpose is to fit the selected models (linear, lasso, and ridge) on the train data and cross-validate their predictive strength on the split test data, as a precursor to evaluating the model with actual test/unseen data. This validation provides the opportunity to choose the best among the predictive models or reevaluate the features selection and interactions. Given the variety of the order of magnitude of the features, a `scaling` exercise was needed.

#### Model evaluation and iteration

The first model, with the full load of features, performed extremely poorly with the linear regression, but as expected relatively strongly with lasso and to a lesser extent with ridge. This did not make it any good, given that the resulting RMSE was too big, as measured by the low ranking this first model received in the Kaggle competition.

At this stage, the correlation matrix was looked at more closely. Only 13 features were selected as offering a relatively strong correlation with the `saleprices`. the other features, on their own, presented no predictive information, only noise, and as such impacted negatively the quality of the model.
An additional iteration was made based on the multicollinearity between certain variables, which resulted in, further, dropping four features. These features were strongly correlated to  other features, which were the once, actually, correlated to `saleprices`.
As a final boost to the model, PolynomialFeatures was used to play the interactions between the most important features. This iterative process was clearly in the right direction as the rank of the model moved from 87, to 65, to 47, to 41.

#### Model (re)visualization

The production model is not perfect. A visualization of the `predictions`(y_hat) plotted against the actual `saleprices`(y) show outliers, suggesting a widening gap in residuals for high-priced properties/luxury homes. It indicates, that the model, in its current version, does not account well for the specificities of these properties. This further suggests that non-selected features, or some interactions between these non-selected features and the selected features could have helped highlight an important impact on the `saleprices`. Alternatively, a more curved model, one that takes an exponential form toward the end of the price spectrum could be considered, failing which, a separate linear regression model could be explored for that category of homes.

### Final recommendations and future steps
This report highlighted the steps undertaken to rebuild missing values and format the data in a way that is ready for visualization, correlation analysis, and predictive modeling. The report also describes the steps undertaken to strengthen the model, from dummy variables, to dropping low correlated features, to reducing multicollinearity, and finally to interacting the selected variables using PolynomialFeatures. This exercise, however, stops short at narrowly predicting the prices of high-end properties.
An extension of this work would be to:
  - test the impact of **interaction terms** with the previously selected features with other features not yet-selected. The result of this exercise could well generalize to the prediction of home values in other cities. it could also serve as reference to homeowners and realtors to know the impact of certain features, including home improvements, on the prices of homes
  - explore **grid searching** capabilities that would **tune the hyperparameters** (testing 2nd and 3rd degrees, etc.) of the regularization models used, to include high-end homes by allowing a more exponential allure to the linear regression towards high prices, and therefore generalize the model to the whole spectrum of residential properties.


## Attachments:
please find attached to
- this executive summary:
- a Jupyter notebook with the model code
- kaggle submission snapshot and score
- the predictions csv file along with the original dataset
- Presentation slides
    
