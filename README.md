# Big Data Analytics using R
## Master of Data Science at Birkbeck, University of London, 10/2018

### Syllabus 
1. Introduction to R
2. Basic Statistics
3. Linear Regression
4. Logistic Regression
5. Cross Validation
6. Decision Trees
7. Ensemble Methods
8. SVM
9. Clustering
10. Dimension Reduction
11. Applications

## Week 1: Introduction to R
**rm(list=ls())** removes everything in the environment

## Week 2: Descriptive statistics
Descriptive Analysis

#### 1. Univariate vs. Bivariate

  * Single value vs. relationship between paris of variables 

#### 2. Variance vs. Standard Deviation
  1. Variance (s2(sample); σ2(population))
      * The average of the squared differences from the mean

  2. Standard Deviation (s(sample); σ(population)) 
      * Equals to square root of variance

#### 3. Biased vs. unbiased sample variance
* Biased sample variance is divided by **n**;
* **Unbiased** sample variance is divided by **n-1**;
* The biased sample variance (↓) usually underestimates the population variance (↑)
  + The observations of a sample fall, on average, closer to the sample mean than to the population mean
  + Using n-1 instead of n as the divisor corrects that by making the result a little bit bigger

#### 4. Covariance vs. correlation

  1. Covariance is a dimensional quantity
      * The value depends on the units of the data
      * Difficult to compare covariances among data sets that have different scales.
      * Covariance = Σ (Xi- Xavg)(Yi-Yavg) / N
      * use **N for population, n-1 for samples**
      * Covariance measures how much the movement in one variable predicts the movement in a corresponding variable
         * **Positive** covariance indicates that **greater** values of one variable tend to be paired with **greater** values of the other variable.
         * **Negative** covariance indicates that **greater** values of one variable tend to be paired with **lesser** values of the other variable.
  2. Correlation is a dimensionless quantity
      * Always between -1 and 1
      * Facilitates the comparison of different data sets
      *  correlation of X and Y =
covariance of X and Y /
(standard deviation of X * standard deviation of Y)




#### 5. In R
1. **var()** and **sd()** in R uses *n-1* as denominator. 
2. Interquartile Range is Q3 - Q1
3. **set.seed(m)** reproduces the exact same set of random numbers as long as the arbitrary integer argument m stays the same.
4. **rnorm(n,mean=0,sd=1)** generates a vector of random normal variables
  * n: sample size
  * default mean=0 and sd=1
  * each time different




## Week 3: Simple Linear Regression
Three big questions for this week:
1. How to estimate?
2. How to assess accuracy of the coefficient estimates (Hypothetis Testing)
3. How to assess accuracy of the model


#### Step 1: How to estimate:
1. Residual sum of squares
2. Least square line:  
    1. Sum of the residuals equals 0
    2. Residual sum of squares is minimised
    least square estimates 

3. How close is a single sample mean `Ƹ𝜇` to the population mean `μ`?  
    * Answer: Use standard error (SE): the average amount that this estimate `ො𝜇` differs from `μ`
    * The more observations we have, the smaller the Standard Error is     

#### Step 2: How to assess accuracy of the efficient estimates (Comparing coefficients only)

Three lines:  
1. True relationship line: `y = f(x)+ ε`
2. Population regression line: `y = b0 + b1x + ε`
   *Popluation regress line is the best **linear** approximation to the true relationship between X and Y
3. Least square line: `y(with hat) = 𝛽0(with hat) + 𝛽1(with hat)x`

#### Standard error (SE)
Standard error is the average amount that this estimate 𝜇-hat differs from μ.  

```SE= variance / n```

The more observations we have, the smaller the SE is. 

#### Hypothesis Tests
Is `B1 = 0` or not? If we can't be sure that B1 `!= then` there is no point using X as the predicto. 

1. **Null hypothesis** - There is no relationship between X and Y

2. **Alternative hypothesis** - There is some relationship between X and Y

3. The higher **t-value** is (equivalently p-value is small), the more possible X and Y are related, then we can be sure that B1(hat) is not 0.
  * We can reject the Null Hypothesis.
  * We declare a relationship to exist between X and Y.
  
4. **P-value**: P values evaluate how well the sample data support that the null hypothesis is true. It measures how compatible your data are with the null hypothesis
  * A smallp-value (typically ≤ 0.05) indicates yoursample provides strong evidence against the null hypothesis, so you reject the null hypothesis.
  * A largep-value (> 0.05) indicates weak evidence against the null hypothesis, so you fail to reject the null hypothesis.
  * Typical p-value cutoffs for rejecting the null hypothesis are 5 or 1%  

5. Summary of t-value and p-value  
  * The t-test produces a single value,t, which grows larger as the difference between the means of two samples grows larger;  
  * t does not cover a fixed range such as 0 to 1 like probabilities do;
  * You can convert a t-value into a probability, called a p-value;  
  * The p-value is always between 0 and 1 and it tells you the probability of the difference in your data being due to sampling error;  
  * The p-value should be lower than a chosen significance level (0.05 for example) before you can reject your null hypothesis.


#### Step 3: How to assess accuracy of the model
1. Residual Standard Error (RSE)
  *  It measures the degress to which the model fits the data (e.g. should this be linear vs. non-linear regression?)
  *  RSE is the estimate of the standard deviation of `ε`
  *  RSE has a unit, and it has the same unit as `Y`
  *  Quantifies average amount that the response will deviate from the population regression

2. Measuring the extent to which the model fits the data  
  R<sup>2</sup> statistic
  * Some of the variation in Y can be explained by variation in the X’s and some cannot.
  * R<sup>2</sup> tells you the **proportion of variance** of Y that can be explained by X.
  * **The higher the R<sup>2</sup>, the better fit the model is.**
  * In simple linear regression, R<sup>2</sup> == Cor(X,Y)<sup>2</sup>

3. `Cor(X,Y) = 0` means there is no **linear** relationship between X and Y, but there could be other relationship.

4. Multiple R-squared and adjusted R-squared:
  * Model with multiple variables: use adjusted R-squared 
  * Model with single variable: use R squared and adjusted R squared interchangably 
  * Generally **use adjusted R-squared** as preference

5. Predicting mean is a lot more accurate than predicting an individual

6. **Prediction interval (PI)** is an estimate of an interval in which future observations (particular individuals) will fall, with a certain probability, given what has already been observed.

7. **Confidence intervals** predict **confidence intervals** for the **mean**, **prediction intervals** for the **individuals**.

Confidence interval is between (the lines are lower than) prediction interval.

#### Conclusion
1. Practical Interpretation of `y-intercept`:
* predictedyvalue when x= 0–no practical interpretation if x= 0 is either nonsensical or outside range of sample data


#### Assignment in Week 3's presentation:
```{r}
fert = c(4,6,10,12)
yield=c(3.0,5.5,6.5,9.0)
FertYield=data.frame(fert,yield)
fert.fit<-lm(yield~fert,data=FertYield)
predict(fert.fit,data.frame(a=(c(2.5,5.5,8.5))),interval="confidence")
confint(fert.fit)
summary(fert.fit)
```


## Week 4 Logistic Regression
Regression vs. Classification

#### Step 1. Come up with `b0 hat` and `b1 hat` to estimate `b0` and `b1` (i.e. How to estimate coefficients)

* Use **maximum likelihood**

We try to find `b0 hat`  and `b1 hat` such that plugging these estimates into
yields
  + a number close to `1` for all individuals who chose Innocent, and
  + a number close to `0` for all individuals who did not choose Innocent.
  + use likelihood function to maximise likelihood 

* Interpreting `b1`

  + If `b1` = 0, this means that there is no relationship between Y and X.
  + If `b1` > 0, this means that when X gets larger so does the probability that `Y = 1`, that is, X and Pr(Y =1) are <u>positively correlated</u>.


#### Step 2. Are the coefficients significant? (Hypothesis Test)
* Is `b1` equal to 0? - null hypothesis
  + In linear regression, we use `t-test`: the higher `t-value` is, the better it is.
  + In logistic regression, we use `z-test`: the higher `z-value` is, the better. 
  + `p-value` is interpreted the same way:
    + If `p-value` is tiny, reject `H0` → there is relationship between `X` and `Pr(Y=1)`
    + Otherwise, accept `H0` → there is no relationship between `X` and `Pr(Y=1)`

+ How sure are we about our guesses for `b0` and `b1`?

#### Step 3. How to make predictions?

#### Case Study: Credit Card Default Data

Qualitative Predictors in Logistic Regression

  * We can predict if an individual default by checking if s/he is a student or not. Thus we can use a qualitative variable “student” coded as (Student = 1, Non-student =0). How?
  መ
  * `b` is positive: This indicates students tend to have higher default probabilities than non-students








## Week 5: Assessing Model Accuracy & Cross Validation
1. How to assess model accuracy
  * For a **regression** problem, we used the **MSE** to assess the accuracy of the statistical learning method
  * For a **classification** problem we can use the **error rate**(e.g. ConfusionMatrix).

2. **Residual sum of squares(RSS)**: The sum of the squares of residuals. It is a measure of the discrepancy between the data and an estimation model. A small RSS indicates a tight fit of the model to the data.

3. A common measure of accuracy is the **mean squared error (MSE)**, which is equal to `1/n * RSS`

4. Our method has generally been designed to make MSE small on the training data we are looking at:
  * e.g. with linear regression we choose the line such that MSE (RSS) is minimisedàleast squares line.

5. Training vs Test MSE

  * In general, the **more flexible** a method is, the lower its **training MSE** will be.
  * However, the test MSE may in fact be higher for a flexible method than a simple approach (e.g. linear regression)

6. Bias/Variance tradeoff
  * **Bias** refers to the error that is introduced by modeling a real life problem (that is usually extremely complicated) by a much simpler problem.
    + The more flexible/complex a method is the less bias it will generally have.
  * **Variance** refers to how much your estimate for f would change by if you had a different training data set (from the same population).
    + The more flexible a method is the more variance it has.

7. Expected test MSE
  * `ExpectedTestMSE = Bias^2 +Var+ σ^2`. `σ^2` is irreducible error. 
  * We want to minimise `ExpectedTestMSE`.
  * It is a challenge to find a method for which both the variance and the squared bias are low.

8. How to calculate MSE in R?
  Consider the linear regression models, this calculates the training MSE:
  ```r
  lm.fit <- lm(y~x,data=DS) 
  mean((y-predict(lm.fit,DS))^2)
  ```

9. For classification models, we'll use Confusion Matrix/Error Rate

  `Accuracy = # correct predictions / total # of predictions`
  `Error rate = # wrong predictions / total # of predictions`

10. How to Calculate Error Rate in R?  
  In logistic regression, calculate the training error rate
  * Building the `glm.fit`
  * Using `glm.fit` to make probability predictions
  * Set a threshold (could be 0.5, or other number) to make qualitative
  predictions based on the probability predictions
  * Using `table()` function to build a confusion matrix
  * Using `mean()` function to calculate the error rate


  ```r
  glm.fit <- glm(default~balance,data = Default, family=binomial) dim(Default)
  #[1] 10000 4
  glm.probs <- predict(glm.fit, Default, type="response") 
  glm.pred <- rep("Yes",10000)
  glm.pred[glm.probs<.5] <- "No" table(glm.pred,default)
  default
  glm.pred 

      No Yes
  No 9625 233 
  Yes 42 100


  # Accuracy
  mean(glm.pred==default)
  [1] 0.9725
  # Error rate
  mean(glm.pred!=default)
  [1] 0.0275
  ```

11. Cross Validation
  * Estimate the test error rate by
    + holding out a subset of the training observations from the fitting process, and then
    + applying the statistical learning method to those held out observations.

  * Cross Validation on Regression Problems
    + The Validation Set Approach
    + Leave-One-Out Cross Validation
    + K-fold Cross Validation
      + Bias-Variance Trade-off for k-fold Cross Validation

 * Cross Validation on Classification Problems

12. **Validation Set Approach**: randomly spliting the data into training part and validation(testing, or hold-out) part

  How to do it?
  * Randomly split Auto data set (392 obs.) into training (196 obs.) and validation data (196 obs.)
    ```r
    set.seed(1)
    train <- sample(392,196)
    ```

  * Fit the model using the training data set

  ```r
  lm.fit.train <- lm(mpg~horsepower,data=Auto,subset=train)
  ```

  * Then, evaluate the model using the validation data set

  ```r
    mean((Auto$mpg-predict(lm.fit.train,Auto))[-train]^2) 
    [1] 26.14142
  ```

  Plot the observations and linear relationship between mpg and horsepower:

  ```r
    plot(Auto$horsepower, Auto$mpg, xlab="horsepower",
    ylab="mpg",
    col="blue") abline(lm.fit.train,col="red")
  ```

  Improving the model using **quadratic** model. Evaluate the model using validation data set([-train] means that we will only use the test dataset): 
  ```r
    set.seed(1)
    train <- sample(392,196)
    lm.fit2.train <- lm(mpg~poly(horsepower,2),data=Auto, subset=train)
    mean((Auto$mpg-predict(lm.fit2.train,Auto))[-train]^2) 
    [1] 19.82259 
    #linear model's MSE: 26.14142
  ```

  The quadratic model has a smaller test error, thus it is better than the simple linear regression model. 

  If test MSEs are very different from each other, it means that this model has high variance. 

  * The Validation Set Approach
  
    + Advantages:
      + Simple
      + Easy to implement

    + Disadvantages:
      + The validation MSE can be highly variable
      + Only a subset of observations are used to fit the model (training data). Statistical methods tend to perform worse when trained on fewer observations.

13. **Leave-One-Out Cross Validation (LOOCV)**

  * This method is similar to the Validation Set Approach, but it tries to address the latter's disadvantages. 
  * For each suggested model, do:
    + Split the data set of size `n` into:
      + training data set size: `n-1`
      + testing data set size: `1`
    + Fit the model using training data set 
    + Validate model using the testing data, and compute the corresponding MSE
    + Reeat this process `n` times
    + Calculate the average of the MSEs = `1/n * MSE`

  LOOCV vs. Validation Set Approach
  * Advantage: LOOCV has less bias
    + We repeatedly fit the statistical learning method using training data that contains `n - 1` obs., i.e. almost all the data set is used
  * Advantage LOOCV produces a less variable MSE 
    + The validation set approach produces different MSE when applied repeatedly due to randomness in the splitting process
    + Performing LOOCV multiple times will always yield the same results, because we split based on 1 obs. each time
  * Disadvantage: LOOCV is computationally intensive 
    + We fit a model n times!

   How to do LOOCV in R:
   Using the Auto data set again, building a linear model 
   
   ```r
    glm.fit <- glm(mpg~horsepower,data=Auto)
    # This is the same as lm(mpg~horsepower,data=Auto)
    library(boot) 
    #cv.glm() is in the boot library
    cv.err <- cv.glm(Auto,glm.fit)
    # cv.glm() does the LOOCV
    cv.err$delta
    [1] 24.23151 24.23114 #(raw CV est., adjusted CV est.) 
    #The MSE is 24.23114 (use the adjusted CV value).
   ```

14. **K-fold Cross Validation**

  * LOOCV is computationally intensive, so we can run k-fold Cross Validation instead
  * With k-fold CV, we divide the data set into k different parts (e.g. k = 5, or k = 10, etc.)
  * We then remove the first part, fit the model on the remaining k-1 parts, and see how good the predictions are on the left out part (i.e. compute the MSE on the first part)
  * We then repeat this k different times taking out a different part each time
  * By averaging the k different MSE’s, we get an estimated validation (test) error rate for new observations

  How to do K-fold validation in R:
  ```r
    glm.fit <- glm(mpg~horsepower,data=Auto)
    # This is the same as in LOOCV
    library(boot)  # This is the same as in LOOCV
    cv.err <- cv.glm(Auto,glm.fit, K=10)
    #K means K-fold, can be 5, 10 or other numbers
    cv.err$delta
    [1] 24.3120 24.2926
  ```  
  The MSE is `24.3120`.

15. Comparing LOOCV and K-fold Cross validation
  * LOOCV is **less bias** than k-fold CV (when k < n)
    + LOOCV: uses n-1 observations
    + K-fold CV: uses (k-1)n/k observations
  * But, LOOCV has **higher variance** than k-fold CV (when k < n)
    + The mean of many highly correlated quantities has higher variance
  * Thus, there is a trade-off between what to use
  * Conclusion: we usually use K-fold (k=5 or k=10)

16. Cross validation for classification problems
  We can use cross validation in a classification situation in a similar manner
  * Divide data into k parts
  * Hold out one part, fit using the remaining data and compute the **error rate** on the held out data
  * Repeat k times
  * CV error rate is the average over the k errors we have computed

## Week 5: Decision Trees
## Week 6. Ensemble Methods
## Week 7. SVM
## Week 8. Clustering
## Week 9. Dimension Reduction
## Week 10. Applications