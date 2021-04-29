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

- Test the model to predict house prices in King County.

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

Step 4: Run a base model
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

A simple way to identify these two variables is by plotting a scatter matrix. Continuous variables show a linear and even distribution across the plot. While categorical variables show a grouped and ordered distribution across the plot. There are also oridinal variables which are ordered-categorical variables. These are categorical classes with a natural order of progression and does not need to be transformed into dummy variables. 

![Scatter Matrix](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/Scatter_Matrix.png)

Here, you can clearly see the two types of data. We can take a closer look at each one of the variables below.

#### Continuous variables

![Continuous Variables](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/Continuous_Variables.png)

The histogram of the continuous variables show a high positive skewness with a bunch outliers extending the tail towards the right. We can remove these outliers using some Z-score calculation.

The resultant histogram below shows clear improvement in the normality of the data. We will take this forward to fit the model.

![Continuous Variables 2](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/Continuous_Variables_2.png)

#### Categorical variables

![Categorical Variables](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/Categorical_Variable.png)

The categorical variables also show presence of outliers. Within these variables we also have so called 'oridnal variables'. These variables have a natural order of progression and does not need to be transformed into dummy variables. We can only use the Z-score calculation on continous or ordinal varibles. We will have to the trim the rest of the categoricals manually.

![Categorical Variables_2](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/Categorical_Variable_2.png)

![Categorical Variables_3](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/Categorical_Variable_3.png)

The scatterplot shows better distiction among classes for the categorical variables. 

#### EDA 2. Check for multicollinearity and remove highly correlated pairs from the dataset

The dataset now needs to be checked for multicollinearity. Having high correlation means that predictors have linear relationship with each other. This leads to predictors adding less value or being insignificant to the model. 

A heatmap can be used to plot the correlation matrix.

![Correlation Matrix](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/Correlation_Matrix.png)

![Correlation Matrix_2](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/Correlation_Matrix_2.png)

You can see from the colormap that there are some pairs which are highly correlated to each other (closer to one). We can sort these out through some code.

![Correlation Matrix_3](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/Correlation_Matrix_3.png)

The resultant heatmap above after removing pairs with over .7 correlation shows some improvement in the data.

#### EDA 3. Finalize the model and plot the line of best fit to predict the price

We will use the statsmodel module to run the base model. The OLS regression in statsmodel gives us a line of best fit minimizing the sum of squared vertical distances between the observed values and the values predicted by the linear approximation. This can be plotted using sns.regplot from seaborn library.

![Multivariate Regression](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/Multivariate_Regression.png)

From the above plot, we can see that there is a high dispersion of data after the million dollar mark. We can reduce the range of house prices over a million to fix this and improve model performance.

![Multivariate Regression](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/Multivariate_Regression_2.png)

The line of best fit looks more in-line with the data for this regression.

### Conclusion

Based on the data available, our final model shows some meaningful relationships on how different variables affect the overall **Price** of a house. The following characterstics have a positive relationship with Price and help increase the value of a home.
* Sqft Lot                                   **+ $1.5k**       
* Number of Bedrooms                         **+ $27k** 
* Number of Bathrooms                        **+ $38k** 
* Condition of the house                     **+ $24k** 
* Grade of the house                         **+ $77k** 
* Number of times the house has been viewed. **+ $41k**  

* Number of floors seem to have a negative relationship with the price of a house, which is odd. This could mean that people in King County prefer houses with lesser floors. However, statistically speaking our data has majority of houses with only one floor and decreases in count as the number of floors increases. This might have created a bias for 'Floors' in our model.   **- $8k**

* Houses built before the year of 1945 seem to have a positive relationship with Price. It can be explained that these houses might have been preserving their value since they are over 50 years of age and are considered as historic.  **+ ($12k - $27k)**

* Houses built after 1945 have a decreasing negative relationship with Price. This confirms the market notion that old houses have lesser value than the new ones. **- ($13k - $25k)**

The relationship between different **Zipcodes** and Price shows the overall distribution of expensive houses to cheaper ones in King County. The top 5 zipcodes with the highest home values are as follows:
* Zipcode_98039	**+ $668k**
* Zipcode_98004 **+ $506k**
* Zipcode_98040	**+ $432k**
* Zipcode_98112	**+ $400k**
* Zipcode_98109 **+ $381k**

While the least desirable zipcodes are as follows:
* Zipcode_98023	**- $20k**
* Zipcode_98092	**- $19k**
* Zipcode_98002	**+ $7k**
* Zipcode_98198	**+ 17K**
* Zipcode_98058 **+ 34k**
