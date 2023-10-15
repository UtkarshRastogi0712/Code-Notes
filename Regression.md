#AIML 
Statistical methods to relate dependent variables with independent variables.
### Types:
- Linear
- Logistic
- Lasso
- Ridge

### Linear:
Linear Regression brings about a linear relationships between a dependent variable and an independent variable. It is used to predict a value from a continuous range of datapoints. 
##### Assumption:
- Assumes a linear relationship
- Mean of residuals is zero
- Residuals have a constant variance over the entire range of values
- Parameters should not have multi-co-linearity (Should be homoscedasticity)
- Residuals should be in a normal distribution (Lack of outliers)

_Formula:_  $$Y=(B_0+B_1X)$$
>Where:
>- $B_0$ is the bias or Y intercept
>- $B_1$ is the coefficient or weight
>- $Y$ is the predicted value
>- $X$ is the Independent variable

_Multivariate linear regression:_ $$Y = B_0 + \Sigma (B_iX_i)$$

_Residual Sum of Squares:_ A residual is the Euclidean distance between the fitted regression line and the Independent variable. Residual Sum of Squares (RSS) is the squared sum of all the residuals.

_$R^2$ Statistic:_ is the metric of correlation between the Independent variable and the Dependent Variable. It describes how much of the Dependent variable is explained by the Independent Variable. 
$$R^2 = \frac{MSS - RSS}{MSS}$$
>Where:
>- MSS is Mean Sum of Squares: $$ MSS = (x_i - \bar{x})^2 $$
>- RSS is Residual Sum of Squares: $$ RSS = (y_p - y)^2$$

*$R^2$ signifies the degree of correlation.* A value of 0 signifies there is no relations between the Dependent and Independent Variable. A value of 1 signifies that the Independent Variable describes the Dependent Variable Completely.

### Logistic:
Logistic Regression is used to classify continuous datapoints into discrete classes. It uses a sigmoid curve to 




