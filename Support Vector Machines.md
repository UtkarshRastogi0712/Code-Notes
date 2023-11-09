#AIML 
Support Vector Machines are suitable models to classify high dimensional data (say n dimensions) by using hyperplanes (n-1 dimensions).

### Three types of SVM:
- Maximum margin classifier
- Support Vector Classifier
- Support Vector Machine

### Maximum Margin Classifier:
It is an optimization problem that tries to maximize the margin (separation) between the hyperplane and the datapoints.

For an N-dimensional space:
- _Hyperplane:_ $$\beta_0 + \beta_1X_1 + \beta_2X_2 ...+\beta_nX_n = 0 $$
>where, $$\beta_0 + \beta_1X_1 + \beta_2X_2 ...+\beta_nX_n \ge M $$
for all datapoints of one class (normal vector length $\ge$ M) and 
$$\beta_0 + \beta_1X_1 + \beta_2X_2 ...+\beta_nX_n \le M $$
for all datapoints of the other class (normal vector length $\ge$ M but in opposite direction)


- _Objective Function to be maximized:_ Find $\beta_0$ , $\beta_1$ , $\beta_2$, ... $\beta_n$ to maximize M
- _Constraint 1:_ To ensure that the normal vector of datapoint from the Hyperplane is of unit length $$\sum_{j=1}^{n} \beta_j =1$$
- _Constraint 2:_ To ensure normal vectors of all datapoints from Hyperplane fall on the right side, we multiply by y which is the class variable = {-1,1} $$y_i(\beta_0 + \beta_1X_i1 + \beta_2X_i2 ...+\beta_nX_in) \ge M $$ $$y_1 ... y_n \epsilon \{-1,1\}$$
__Drawback of Maximum Margin Classifier:__ 
- Does not work for non separable classes
- Very susceptible to outlier that are close to the other class by far from their own.

### Support Vector Classifier:

Support Vector Classifier build on the idea from Maximum Margin Classifier but fixes its drawbacks by allowing features to be classified in the wrong class up to a certain threshold. 

The hyperplane equation, objective function and constraint 1 remain the same. 

- _Constraint 2:_ We add a scaling factor for the normal vector from the hyperplane in the form of $(1-\epsilon_i)$
$$y_i(\beta_0 + \beta_1X_i1 + \beta_2X_i2 ...+\beta_nX_in) \ge M(1-\epsilon_i) $$
- _Constraint 3:_ We ensure that the total magnitude of wrong classifications stay under a threshold (C) and the deviation is only counted from datapoints classified wrong.

$$\epsilon_i \ge 0$$
$$\sum_{i=1}^{m}\epsilon \le C$$
Where, C is a non negative tuning parameter to tune the magnitude of error that the model can accommodate. 
> Margin width is directly proportional to C

### Support Vector Machines:
Support Vector Machines come into play when the datapoints are impossible to separate linearly in the given n dimensional space and no amount of tradeoff in Support Vector Classifier does the trick. We use Kernel Functions in SVM to elevate the n dimensional feature space to n+1 dimensions to try and separate the datapoints. 

>Ex: A feature space with one class enclosed inside a unit circle and the other class outside the unit circle in 2 Dimensions (X,Y) can be mapped into a 3 Dimensional space ($X^2$,$Y^2$,$XY$) to be separable.

#### Kernel Functions:
These are used to approximate the transformation of lower dimension feature sets into higher dimensions without having to undertake all the matrix transforms linked with it. The main idea is that the basis function to be optimized is dependent on $X^TY$ so instead of finding Higher dimensional features, we can use a kernel to approximate $\phi(X^T)\phi(Y)$.

$$K(X,Y) = <\phi(X),\phi(Y)> = \phi(X^T)\phi(Y) $$
Examples:
- _Linear kernel:_ $$\phi(x,y)= (x^Ty) $$
- _Polynomial kernel:_  $$\phi(x,y)= (x^Ty + R)^D $$
- _Radial Basis Function:_ $$\phi(x,y) = e^{-\gamma||x-y||^2}$$