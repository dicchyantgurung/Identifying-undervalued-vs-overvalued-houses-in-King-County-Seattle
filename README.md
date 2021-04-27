# King County Housing Sales Analysis

![King County](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/KC.jpg)

### Project: 

Clean, explore, and model this dataset on a multivariate linear regression to predict the sale price of houses as accurately as possible.

### Dataset:

King County Housing Sales Data

### Objective:

#### EDA 1. Identify continuous vs categorical variables and transform them accordingly

- The data set consists of many predictors which are both continuous and catgorical in nature. For us to perform a multivariate linear regression,
these will need to be cleaned, trimmed and transformed appropriately before fitting them into a model.

#### EDA 2. Check for multicollinearity and remove highly correlated pairs from the dataset 

- Multicollinearity reduces predictive power or significance of the predictors. Having a model without multicollineraty means that each of the predictors have an
independent contribution to the overall result of the model.

#### EDA 3. Finalize the model and plot the line of best fit to predict the price

- Finally, test the model to predict house prices in King County.

### Process Overview:

Step 1: Clean the data
- Remove or fill missing values
- Remove unwanted columns

Step 2: Pre-process the data
- Identify continous vs categorical data
- Remove outliers
- Create ranges for some categorical variables
- Transform categoricals into dummy variables
- Merge continous and transformed categorical variables to create a final preprocessed dataframe

Step 3: Check for multicollinearity
- Run correlation matrix and remove highly correlated pairs
- Plot to confirm correlation

Step 4: Run a base linear model
- Perform linear regression to identify p-values among predictors
- Remove any predictor with p-value larger than 5%
- Perform k-folds cross validation to validate the model
- Plot the model

Step 5: Tune the base model
- Trim the 'Price' column to only include data upto 1 million dollars
- Perform k-folds cross validation to validate the model
- Finalize the model

Step 6: Predict the price
- Using the coefficients generated by the model, predict the sale price of random houses


### EDA 

#### EDA 1. Identify continuous vs categorical variables and transform them accordingly

After the data has been cleaned by removing the missing values, we need to separate the continuous and categorical variables to prepare them for regression.

A simple way to identify these two variables are by plotting a scatter matrix. Continuous variables show a linear and even distribution across the plot. While categorical variables show a grouped and ordered distribution across the plot. There are also oridinal variables which are ordered categorical variables. These are categorical classes with a natural order of progression and does not need to be transformed. INSERT IMAGE HERE

The continuous variables show a high positive skewness with a bunch outliers extending the tail towards the right. We can remove these outiers using the Z-score calculation.
INSERT IMAGE HERE

The histogram shows clear improvement in the normality of the data. We will take this forward to fit the model.

The categorical variables also show presence of outliers. Within these variables we also have so called 'oridnal variables'. These variables have a natural order of progression and does not need to be transformed into dummy variables. We can only use the Z-score calculation on continous or ordinal varibles. We will have to the trim the rest of the true categoricals manually.

INSERT IMAGE HERE

The scatterplot shows better distiction among classes for the categorical variables. 

#### EDA 2. Check for multicollinearity and remove highly correlated pairs from the dataset

The dataset now needs to be checked for multicollinearity. Having high correlation among each other will lead to predictors being dependent and loses their true significance within the model. 





