# Linear Regression

Credits: DATAtab, Delina Ivanova

### What is it?

Linear regression is a type of regression method that can be used to solve regression tasks. There are 2 types, simple and multiple linear regression:
* Simple linear regression consists of a single predictor/independent variable and a single target/dependent variable.
* Multiple linear regression consists of a single target/dependent variable and more than 1 predictor/independent variables.

### What do we use it for?

Linear regression can be used to either measure the influence of one more variables on another variable, or predict one variables using one or more other variables.

### How does it work?

#### Simple Linear Regression

We will begin by first explaining simple linear regression. Here we will refer to our target variable as y, and our predictor variable as x, we are attempting to use x to predict y. Note that linear regression does make many assumptions, these will be noted below.

We will be utilizing the following equation: $\hat{y} = ax + b$. You will notice that this is the equation of a line, we are trying to fit a line through the data that minimizes the error made (error is considered to be the perpendicular distance of each point to the line).

We can calculate $a$ and $b$ as such: $$a = r * (\sigma_y / \sigma_x)$$ $$b = \bar{y} - a * \bar{x}$$

Note that $a$ can be thought of as representing how much the dependent variable would change if the independent variable changed by 1 unit. Whereas $b$ can be thought of to be what the dependent variable should if the independent variable is 0.

Where $r$ is the correlation of x and y, $\sigma$ represents the standard deviation, $\bar{y}$ is the mean of the y data, and $\bar{x}$ is the mean of the x data. In the case of simple linear regression these values can be easily computed by hand. Note that $a$ could also be simply computed as the slope if a line of best fit is drawn by hand before calculations are made, but this is not a typical practice in data science.

A regression error term, $\epsilon$, can be added to the regression equation, such that it becomes: $\hat{y} = ax+b+\epsilon$. This error can be calculated as the difference between the calculated value and the actual value (in some cases it may be computed using a distance metric).

This regression equation can now be used to predict values of y for given values of x.

#### Multiple Linear Regression

In the case of multiple linear regression, the equation would take the following form: $\hat{y} = a_1x_1 + a_2x_2 + ... + a_kx_k + b$. 

Computing the coefficients $a$ and value of $b$ is no longer as easy as it was in the case of simple linear regression. This is done usually through ordinary least squares (OLS) or general least squares (GLS), both of which will be receiving their own entries in the near future.

#### Interpreting Results of Linear Regression

$R$ or the *Multiple Correlation Coefficient* represents the correlation between the dependent and independent variables.

$R^2$ or the *Explained Variance* indicates how much of the variance of the dependent variable can be explained by the independent variable(s).

Adjusted $R^2$ is a version of $R^2$ that has been modified to compensate for the tendency of $R^2$ to be overestimated when there are many predictors. It should always be consulted when using multiple linear regression.

To assess the performance of the model we compute the *Mean Square Error* (MSE), this is also known as the *regression standard error* or *residual standard error*. It can be computed as follows: $$MSE = \frac{\Sigma^n_{i=1}(y_i-\hat{y}_i)^2}{n - 2}$$

The regression coefficients will also be returned, these are the actual coefficients assigned to each predictor variable (the $a$ value(s) discussed above). There may be both unstandardized and standardized coefficients, unstandardized are the ones that will appear in your equation, while standardized coefficients have been standardized to allow you to see which predictors are most influential on the target. Along with them will be a p-value for each of them, this p-value tells you if the coefficients are significant or not, if it is less than 0.05 then it is considered significant.

Statistical testing can also be printed out in a model summary, but these metrics will be receiving their own entries at a later date.

#### Assumptions of Linear Regression

Linearity: There must be a linear relationship between the independent and dependent variables.
* Linear regression attempts to draw a straight line through the data, therefore there must be a linear relationship within the data.

Normally Distributed Errors: The error component must be normally distributed.
* The data points above or below the regression line follow a normal distribution, meaning there are more points closer to the regression line than farther away from it.

Multi-Collinearity: There can be no multi-collinearity.
* This occurs when two or more of the predictors are strongly correlated with one another. The effect of the individual predictors can not be separated.
* If we are just using the regression model for prediction, then this assumption can be ignored. However, if we are using the model to determine the influence of the independent variables on the dependent variable, then this assumption must be upheld.
* To test this we can create another regression model, attempting to predict a predictor with the remaining predictors. If the other predictors can predict the predictor correctly, then we do not need said predictor in our model. This would then need to be repeated for each predictor. This is of course a rudimentary way of testing this, many other ways do exist.

Heteroskedasticity: There can be no heteroskedasticity.
* This occurs when the variance of the residuals are not equal. Meaning that the errors at each of the predictors have different variances. Note that the residuals are an error term ($\epsilon$ that was discussed above).
* Ideally we would want to see that the variance of the residuals are equal for all of the predictors.