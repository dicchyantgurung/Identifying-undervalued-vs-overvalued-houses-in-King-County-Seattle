# King County Housing Sales Analysis

![King County](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/KC.jpg)

### Project: 

Clean, explore, and model the dataset on a multivariate linear regression to predict the sale price of houses as accurately as possible.

### Dataset:

King County Housing Sales Data

### Objective:

#### - EDA 1. Identify effects of time on house prices over the years

#### - EDA 2. Identify the most and least desirable neighbourhoods in King County 

#### - EDA 3. Identify the most important factor for a house price in King County

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

Step 5: Extract the coefficients
- Perform reverse log to calculate true values of each predictor

Step 6: Predict the price
- Using the coefficients generated by the model, predict the sale price of random houses


### EDA 

After the data has been cleaned by removing the missing values, we need to separate the continuous and categorical variables to prepare them for regression.

A simple way to identify these two variables is by plotting a scatter matrix. Continuous variables show a linear and even distribution across the plot. While categorical variables show a grouped and ordered distribution across the plot. There are also oridinal variables which are ordered-categorical variables. These are categorical classes with a natural order of progression and does not need to be transformed into dummy variables. 

In the scatter matrix below, you can clearly see the two types of data. We can take a closer look at each one of the variables in the section below.

![Scatter Matrix](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/Scatter_Matrix.png)

#### Continuous Variables

Plotting a histogram for the continuous variables show a high positive skewness. 

![Continuous Variables](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/continuous1.png)

The skewness can be corrected by removing the outliers using Z-score calculation and some manual trimming of data. 
The resultant histogram shows clear improvement in the normality of the data. We will take this forward to fit the model.

![Continuous Variables 2](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/continuous2.png)

#### Categorical Variables

The categorical variables also show presence of some outliers in its data.

![Categorical Variables](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/categorical1.png)

Within these variables we also have so called 'oridnal variables'. We can use the Z-score calculation on these ordinal varibles. However, we will have to the trim the rest of the categoricals manually.

After the outliers are removed, the resultant scatterplot shows better distiction among classes for the categorical variables. 

![Categorical Variables_2](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/Categorical_Variables_2.png)

![Categorical Variables_3](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/Categorical_Variables_3.png)

### Multicollinearity

The dataset now needs to be checked for multicollinearity. Having high correlation means that predictors will have linear relationship with each other. This leads to predictors adding less value or being insignificant to the model. 

A heatmap can be used to plot the correlation matrix.

![Correlation Matrix](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/corr1.png)

Taking a closer look,

![Correlation Matrix_2](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/corr2.png)

We can see from the colormap that there are some highly correlated pairs. The correlation ranges from -1 to 1. 1 being 100% postively related and -1 being 100% inversely related. It is common practise to consider any pairs greater than .7 to be highly correlated. This can be removed through some code.

The resultant heatmap below shows better correlation among the predictors.

![Correlation Matrix_3](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/corr3.png)

### Final Model

We will use the statsmodel module to run the model. The OLS regression in statsmodel gives us a line of best fit by minimizing the sum of squared vertical distances between the observed values and the values predicted by the linear approximation. This can be plotted using sns.regplot from seaborn library.

![Multivariate Regression](https://github.com/dicchyant84/Module_2-Final-Project/blob/main/Graphs/regression.png)

The line of best fit looks more in-line with the data for this regression.

### Conclusion

Based on the regression, our final model shows some meaningful relationships on how different variables affect the overall **Price** of a house. With an overall coefficient of **- $228k**, each of the characterstic's coefficients are added in multiples of their respective quantity, in order to give the final price of a house.

The following characterstics have a positive relationship with Price and helps increase the value of a home.
* Sqft Living **+ $80k** (per 1000 sq ft)
* Sqft Lot **+ $10k** (per 1000 sq ft)      
* Condition of the house **+ $25k**  
* Grade of the house **+ $50k** 
* Number of times the house has been viewed. **+ $35k**  

**Number of Bedrooms** show a negative coefficient in the model. This could be because the model calculates the coefficients considering all factors that lead to a final price of a house. Thus when factoring for Bedroooms is coming up to be negative in terms of price action. Conclusively, our model suggests that higher number of Bedrooms in the same location with similar Sqft Living, Sqft Lot, Condition, Grade, etc is considered to decrease the value of a home. **- $16k**

**Houses built before the year of 1945** seem to have a positive relationship with Price. It can be explained that these houses might have been preserving their value since they are over 50 years of age and are considered as historic. The **houses after 1945** have a decreasing negative relationship with Price, which confirms the market notion that old houses have lesser value than the new ones. **+ ($9k - 24k)**

The relationship between different **Zipcodes** and **Price** shows the overall distribution of home value in King County. 

The top 5 zipcodes with the highest home value are as follows:
* Zipcode_98039	**+ $668k**
* Zipcode_98004 **+ $516k**
* Zipcode_98112	**+ $450k**
* Zipcode_98102	**+ $445k**
* Zipcode_98109 **+ $440k**

While the least desirable zipcodes are as follows:
* Zipcode_98092	**- $20k**
* Zipcode_98023	**- $13k**
* Zipcode_98198	**+ $26k**
* Zipcode_98188	**+ $34K**
* Zipcode_98038 **+ 35k**
