# Ames Housing Pricing Model

## Executive Summary


The objective of this project is to create a regression model based on the Ames Housing Dataset. The model will predict the  prices of unseen sale transactions. 

The Ames Housing Dataset has about 30 different features relating to houses.

Several versions of the model have been submitted to the Kaggle competion. the best scoring model will be the main subject of analysis in this technical report. However, unsuccessful attempts to improve the model will be described, when relevant, as they tried to address a data science problem. 

### Scope of the project:

#### The scope of the valuation exercise is as follows:
  - highlevel exploration of the data, mainly using descriptive analysis and summary statistics
  - identification of missing data, through
  - exploring options to impute data through value_counts and data dictionary
  - study of correlations, through heatmaps and correlation table
  - selection of features
  - dummying the categorical variables
  - feature engeneering through use of polynomials
  - boost performance by dropping multicullinear variables
  
### the Data Science problem: 
  - put the data in an interpretable format which could be used to build a pricing model that would help estimate home prices based on selected features
  
### The Data Science Process

The outline below does not necessarily cover every single thing that you will want to do in your project. You may choose to do some things in a slightly different order. Many students choose to work in a single notebook for this project. Others choose to separate sections out into separate notebooks. Check with your local instructor for their preference and further suggestions.

### the dataset
the dataset is comprised of two csv file, a training set with features and prices, and a test set with just the features. the prices were meant to be unseen. the prices pertaining to the test dataset are the subject of the Kaggle competition predictions. 

#### Exploratory data analysis
##### Identification of missing values or inconsistent data
1. During basic EDA, you identify many missing values in a column/feature.

##### Data descriptive analysis
##### review of the data dictionary
2. You consult the data dictionary and use domain knowledge to decide _what_ is meant by this missing feature.



#### Data cleaning
3. You impute a reasonable value for the missing value.
- Determine _what_ missing values mean.

  - use of data dictionary
  - use of value_counts()  - Identify outliers.
  - use of functions to reproduce the transformations applied to the training set on the test set
  - Figuring out programmatically concise and repeatable ways to clean and explore your data will save you a lot of time.

#### Exploratory visualization: heatmaps, correlation and colinear matrices
4. You plot the distribution of your feature.
    - - Which features appear to add the most value to a home?
to question correlation and relationship across predictive variables
    - include plots

  
### Target audience:
  - The model is designed to be useful tool for a number of stakeholders, including city government, realestate agents and home buyers alike

### Modeling process

Given the continuous nature of the prediction, the distribution sample data and it's residuals, the linear regression model would be the best alternative. 

Among the different alternatives for testing the model, the RMSE is the one that will be used to evaluate the model's strength. 

#### Refining models over time
5. You realize what you imputed has negatively impacted your data quality.
6. You cycle back, re-load your clean data, re-think your approach, and find a better solution.

#### Use of train-test split
#### use of scaling 
#### cross-validation
*** see discription in the course ***


### Model evaluation:
    - - Look at how accurate your predictions are.
consider your evaluation metrics
    - consider your baseline score
    - Does the student test and evaluate a variety of models to identify a production algorithm (**AT MINIMUM:** linear regression, lasso, and ridge)?
  - featur selectio
    - how can your model be used for inference? ** aply that table with p values and confidence intervals
    - Is there a pattern to your errors? Consider reworking your model to address this.

    - a word about outliers: the model shows a clear increase in residual variability at the top spectrum of prices, indicating that the model, in its current version does not cater for the specificities of the high-end homes. This suggests that some interactions with chosen features could have helped highlight a greater impact on the modeling of luxury homes. It could be also that some features, that were ignored alltogether in the general model, would have had an impact on the modeling of luxury home prices. Although the model catered well to the mid-range prices, it did poorly when estimating high priced homes. this suggests that a different linear regression could be explored for those homes. 
    - manually drop colinear features
    - my production model

### Final recommendations and future steps
  - feature combination
  - interaction terms
  - manually drop collinear features?
  - What are things that homeowners could improve in their homes to increase the value?
this model will generalize to other cities
  - the model is good for most houses in the mid-range with ordinary features
  - homebuyers, realestate agents and city governments can use it as indication to pricing, impact of infrastructure, and impact of added features that wold have a higher than proportionate impact, given the cost
  - In these cases, we would like to give the network more expressive power to learn a probability-like number for each possible label value. This can help in both making the problem easier for the network to model. When a one hot encoding is used for the output variable, it may offer a more nuanced set of predictions than a single label.
  - Use elastic net
  - Tune hyperparameters.

  
#### grid searching for hyperparameters
the next step would be to fine tune the hyperparameters in the regularization models used. You would expect that any setting in these regularization would take care of the noise surrounding the price data, but it appeared that it is not the case. An example in case is the use of all features, including categorical, to make the best predictions of prices. The assumption was that, although some of the feature were less important than others, the lasso model would recognize them and actively limit or cancel their effect. It was not what was experienced. The lasso model, using all features, scored very low as a predictor. You may argue that it was to be expected that there is something wrong with setting of the data, given that the linear regression model indicated a problem with the model, at a negative R2. 

## Attachments:
please find attached to 
- this executive summary: 
- Jupyter notebook
- kaggle submission snapshot
- submitted csv file along with the original dataset
- Presentation slides
