# 11.1 THE ESTIMATION TASK

Thus far in the Modeling Phase we have covered the following tasks:

+   - Classification task
+   - Clustering task

There remain two tasks left to cover:

+   - Estimation task
+   - Association task

In this chapter, we cover the estimation task; later, in Chapter 14, we will cover the association task.

The most widespread method for performing the estimation task is linear regression. Simple linear regression approximates the relationship between a numeric predictor and a continuous target, using a straight line. Multiple regression modeling approximates the relationship between a set of p > 1 predictors and a single continuous target, using a p-dimensional plane or hyperplane.

# 11.2 DESCRIPTIVE REGRESSION MODELING

The usual multiple regression model is a parametric model, defined by the following equation:

```
y = β₀ + β₁x₁ + β₂x₂ + ⋯ + βₚxₚ + ε
```

where the x’s represent the predictor variables, and the β’s represent the unknown model parameters, whose values are estimated using the data! Now, estimating

> 'For much more on inferential regression modeling, see Data Mining and Predictive Analytics.