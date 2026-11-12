variables. For this exercise we will use one dummy variable, which equals one if a customer has churned.

```
churn_ind = pd.get_dummies(churn['Churn'], drop_first = True)
```

The get_dummies() command creates two indicator variables, one for each categorical value in Churn. The drop_first = True input will drop the first dummy variable, which corresponds to Churn = False in our case, and retain the remaining dummy variable, which corresponds to Churn = True.

The remaining commands save the new dummy variable as a data frame, add a constant term so our regression model will have a constant, and renames the columns so the output will be easier to read.

```
X = pd.DataFrame(churn_ind)
X = sm.add_constant(X)
X.columns = ['const', 'Churn = True']
```

We also prepare the response variable.

```
y = pd.DataFrame(churn[['CustServ Calls']])
```

Finally, we run Poisson regression using the GLM() command.

```
poisreg01 = sm.GLM(y, X, family = sm.families.Poisson()).fit()
```

Notice the three input values of the GLM() command. The first two, y and X, specify the response variable and predictor variables, respectively. The third, family = sm.families.Poisson(), specifies that Poisson regression should be used. The fit() command will fit the model to our data. We save the result as poisreg01. Use the summary() command to view the results of the model.

```
poisreg01.summary()
```

An excerpt from the output of summary() is shown in Figure 13.5.

# 13.6.2 How to Perform Poisson Regression Using R

As with our Python example, we restrict this section to illustrating how to build the Poisson regression model. We return to the glm() command, which we used previously to build a logistic regression model, to now build a Poisson regression model.

```
poisreg01 <- glm(formula = CustServ.Calls ~ Churn, data = churn, family = poisson)
```