# 6.1  Re-Introduction to Regression

Simple linear regression² builds the model $f(x)=ax+b$ by minimizing the sum of errors squared.³ As an optimization problem, this is

$$\operatorname{Minimize}\ SSE=\sum_{i=1}^{n}(y_i-f(x_i))^2 \qquad (6.1)$$

Most programs will do the computations for (6.1) easily; a calculator can handle small data sets. Excel, JMP, R, SAS, Stata, and SPSS are among the most commonly used programs. We will continue to use Maple.

For the ordinary least squares method of linear regression, we are most concerned, in this chapter, with the mathematical modeling and the use of the model for *explaining* or *predicting* the phenomena being studied or analyzed. Other standard uses are *variable screening* and *parameter estimation*. We will make use of the basic diagnostic measures, percent relative error and residual plots, for analysis. Percent relative error is calculated as

$$\%RE=\frac{y_i-f(x_i)}{y_i}\cdot100. \qquad (6.2)$$

A rule of thumb for the magnitude of percent relative error is that most should be less than 20%, and those near where a prediction is needed should be less than 10%.

A plot of residuals versus the model provides a visualization of the goodness of a model’s fit. Examine the plot for trends or patterns such as those shown in Figure 6.1. If a pattern is apparent, the model is not adequate, even though we might have to use it. If there is no visual pattern, then we may take that as evidence that the model is adequate.

When should we use simple linear regression and when should we use something more advanced? Let’s begin an answer with the concept of *correlation*.

# Correlation

Many decision makers have misconceptions about correlation in linear regression that is often engendered by non-technical, common-usage definitions of the term. *The Oxford English Dictionary* defines

correlation: *noun*

+   1. A mutual relationship or connection between two or more things.