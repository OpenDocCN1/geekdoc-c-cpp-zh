
## EXERCISES

### CLARIFYING THE CONCEPTS

- 1. How does multiple regression approximate the relationship between a set of two predictors and a single numeric target?

- 2. Explain how we are bypassing the classical statistical inference approach to regression.

- 3. Explain why it is not necessary to standardize the predictors when there is only one continuous predictor and the others are flags?

- 4. True or false: Our use of p-values as guides for determining inclusion in the model means that we are using statistical inference. If false, explain why not.

- 5. For the training set results in Figure 11.13, suppose two customers both had a store credit card, but Customer A had 100 more days between purchases than Customer B. Describe the difference in the two customers' estimated sales per visit.

- 6. For the training set results in Figure 11.13, suppose two customers both had the same days between purchases, but Customer C had a store credit card and Customer D did not. Describe the difference in the two customers' estimated sales per visit.

- 7. Calculate the prediction error for Customer 2 in the training set.

- 8. Calculate s for the test data set.

- 9. Calculate the MAE for the test data set.

- 10. True or false: Stepwise regression always finds the optimal set of predictors.

### WORKING WITH THE DATA

For the following exercises, work with the clothing_sales_training and clothing_sales_test data sets. Use either Python or R to solve each problem.

- 11. Use the training set to run a regression model to predict Sales per Visit using Days between purchases, Credit card, and Web account. Identify which predictor variable should not be in the model.

- 12. Validate the model from the previous exercise, by running the regression using the test data set.

- 13. Suppose someone said, “There is no evidence for a relationship between Sales per Visit and whether the customer has a store credit card.” How would you respond?

- 14. Suppose someone said, “There is no evidence for a relationship between Sales per Visit and whether the customer has a store web account.” How would you respond?

- 15. Run a regression model to predict Sales per Visit, using only the variables found to be significant in the previous regression model.

- 16. Validate the model from the previous exercise.

- 17. Use the regression equation to complete this sentence: “The estimated Sales per Visit equals...”

- 18. Calculate and interpret the standard error of the estimate for the regression.

- 19. Find and interpret $R^2_{adj}$.

- 20. Calculate and interpret the MAE for the regression model. Compare it to the standard error.

- 21. Perform stepwise regression on the model in Exercise 11. Confirm that it converges to the model in Exercise 13.

- 22. Calculate $MAE_{baseline}$.

- 23. Compute $MAE_{regression}$.

- 24. Determine whether the regression model outperformed its baseline model.

### HANDS-ON ANALYSIS

For the following exercises, work with the `adult` data set. Use either Python or R to solve each problem.

- 25. Partition the data set into a training set and a test set, each containing about half of the records.

- 26. Run a regression model to predict Hours per Week using Age and Education Num. Obtain a summary of the model. Are there any predictor variables that should not be in the model?

- 27. Validate the model from the previous exercise.

- 28. Use the regression equation to complete this sentence: "The estimated Hours per Week equals ..."

- 29. Interpret the coefficient for Age.

- 30. Interpret the coefficient for Education Num.

- 31. Find and interpret the value of s.

- 32. Find and interpret $R^2_{adj}$.

- 33. Find $MAE_{baseline}$ and $MAE_{regression}$ and determine whether the regression model outperformed its baseline model.

For the following exercises, work with the `bank_reg_training` and the `bank_reg_test` data sets. Use either Python or R to solve each problem.

- 34. Use the training set to run a regression predicting Credit Score, based on Debt-to-Income Ratio and Request Amount. Obtain a summary of the model. Do both predictors belong in the model?

- 35. Validate the model from the previous exercise.

- 36. Use the regression equation to complete this sentence: "The estimated Credit Score equals ..."

- 37. Interpret the coefficient for Debt-to-Income Ratio.

- 38. Interpret the coefficient for Request Amount.

- 39. Find and interpret the value of s.

- 40. Find and interpret $R^2_{adj}$. Comment.

- 41. Find $MAE_{baseline}$ and $MAE_{regression}$, and determine whether the regression model outperformed its baseline model.

- 42. Construct a regression model for predicting Interest, using Request Amount. Obtain a summary of the model.

- 43. Explain what is unusual with your results from the previous exercise.

- 44. Construct a scatterplot of Interest against Request Amount. Describe the relationship between the variables. Explain how this relationship explains the unusual results from your regression model.

For the following exercises, work with the Framingham_training and the Framingham_test data sets. Reexpress Sex so that it is a flag variable with 0 for males and 1 for females. Use either Python or R to solve each problem.

- 45. Use the training set to run a regression predicting Age, based on Sex and Education. Obtain a summary of the model. Do both predictors belong in the model?

- 46. Validate the model from the previous exercise.

- 47. Use the regression equation to complete this sentence: “The estimated Age equals...”

- 48. Interpret the coefficient for Sex.

- 49. Interpret the coefficient for Education.

- 50. Find and interpret the value of s.

- 51. Find and interpret $R^2_{adj}$.

- 52. Find $MAE_{baseline}$ and $MAE_{regression}$, and determine whether the regression model outperformed its baseline model.

For the following exercises, work with the white_wine_training and the white_wine_test data sets. Use either Python or R to solve each problem.

- 53. Use the training set to run a regression predicting Quality, based on Alcohol and Sugar. Obtain a summary of the model. Do both predictors belong in the model?

- 54. Validate the model from the previous exercise.

- 55. Use the regression equation to complete this sentence: “The estimated Quality equals...”

- 56. Interpret the coefficient for Alcohol.

- 57. Interpret the coefficient for Sugar.

- 58. Find and interpret the value of s.

- 59. Find and interpret $R^2_{adj}$.

- 60. Find $MAE_{baseline}$ and $MAE_{regression}$, and determine whether the regression model outperformed its baseline model.

## 12.1 THE NEED FOR DIMENSION REDUCTION

High dimensionality in data science refers to when there are a large number of predictors in the data set. For example, 100 predictors describe a 100-dimensional space. So, why do we need dimension reduction in data science?

- **Multicollinearity.** Typically, large databases have many predictors. It is unlikely that all of these predictors are uncorrelated. Multicollinearity, which occurs when there is substantial correlation among the predictors, can lead to unstable regression models.

- **Double-Counting.** Inclusion of predictors which are highly correlated tends to overemphasize a particular aspect of the model, that is, essentially double-counting this aspect. For example, suppose we are trying to estimate the age of youngsters using math knowledge, height, and weight. Since height and weight are correlated, the model is essentially double-counting the physical component of the youngster, as compared to the intellectual component.

- **Curse of Dimensionality.** As dimensionality increases, the volume of the predictor space grows exponentially, that is, faster than the number of predictors itself. Thus, even for huge sample sizes, the high-dimension space is sparse. For example, the empirical rule states that about 68% of normally distributed data lies within one standard deviation of the mean. But, this is for one dimension. For 10 dimensions, only 2% of the data lies within the analogous hypersphere.

- **Violates Parsimony.** The use of too many predictors also violates the principle of parsimony, the scientific principle one sees in many branches of science, that things often behave in a quite economical way. In data science, simplicity (parsimony) should be considered when comparing models, keeping the number of predictors to such a size that would be easily interpreted.

- **Overfitting.** Keeping too many predictors in the model tends to lead to overfitting, in which the generality of the findings is hindered because new data do not behave the same as the training data for all the many predictors.
