
and where

$t_L = \text{left child node of node } t$
$t_R = \text{right child node of node } t$
$P_L = \frac{\text{number of records at } t_L}{\text{number of records in training set}}$
$P_R = \frac{\text{number of records at } t_R}{\text{number of records in training set}}$
$P(j|t_L) = \frac{\text{number of class } j \text{ records at } t_L}{\text{number of records at } t}$
$P(j|t_R) = \frac{\text{number of class } j \text{ records at } t_R}{\text{number of records at } t}$

Then, the optimal split is whichever split maximizes this measure $\Phi(s|t)$ over all possible splits at node $t$. Thus, CART identified the root node split in Figure 6.1 as maximizing $\Phi(s|t)$ over all candidate root node splits.

### 6.2.1 How to Build CART Decision Trees Using Python

Load the required packages and read in the training data set as adult_tr.

```python
import pandas as pd
import numpy as np
import statsmodels.tools.tools as stattools
from sklearn.tree import DecisionTreeClassifier, export_graphviz
adult_tr = pd.read_csv("C:/.../adult_ch6_training")
```

For simplicity, we save the Income variable as y.

```python
y = adult_tr[['Income']]
```

We have a categorical variable, Marital status, among our predictors. The CART model implemented in the sklearn package needs categorical variables converted to a dummy variable form. Thus, we will make a series of dummy variables for Marital status using the categorical() command.

```python
mar_np = np.array(adult_tr['Marital status'])
(mar_cat, mar_cat_dict) = stattools.categorical(mar_np,
drop=True, dictnames=True)
```

We turn the variable Marital status into an array using array(), then use the categorical() command from the stattools package to create a matrix of dummy variables for each value of Marital status. We save the matrix and dictionary separately using (mar_cat, mar_cat_dict).

The matrix mar_cat contains five columns, one for each category in the original Marital status variable. Each row represents a record in the adult_tr data set. Each row will have a 1 in the column which matches the value that record had in the original Marital status variable. You can tell which column represents which category by examining mar_cat_dict. In our case, the first row of mar_cat has a 1 in the third column. By examining mar_cat_dict, we know the third column represents the "Never married" category. Sure enough, the first record of adult_tr has "Never married" as the Marital status variable value.

Now, we need to add the newly made dummy variables back into the X variables.

```python
mar_cat_pd = pd.DataFrame(mar_cat)
X = pd.concat((adult_tr[['Cap_Gains_Losses']], mar_cat_pd), axis = 1)
```

We first make the mar_cat matrix a data frame using the DataFrame() command. We then use the concat() command to attach the predictor variable Cap_Gains_Losses to the data frame of dummy variables that represent marital status. We save the result as X.

Before we run the CART algorithm, note that the columns of X do not include the different values of the Marital status variable. Run mar_cat_dict to see that the first column is for the value "Divorced," the second for "Married," and so on. Since the first column of X is Cap_Gains_Losses, we can specify the names of each column of X.

```python
X_names = ["Cap_Gains_Losses", "Divorced", "Married",
"Never-married", "Separated", "Widowed"]
```

It will help us when visualizing the CART model to know the levels of y as well.

```python
y_names = ["<=50K", ">50K"]
```

Now, we are ready to run the CART algorithm!

```python
cart01 = DecisionTreeClassifier(criterion = "gini", max_leaf_nodes=5).fit(X,y)
```

To run the CART algorithm, we use the DecisionTreeClassifier() command. The DecisionTreeClassifier() command sets up the various parameters for the decision tree. For example, the criterion = "gini" input specifies that we are using a CART model which utilizes the Gini criterion, and the max_leaf_nodes input trims the CART tree to have at most the specified number of leaf nodes. For this example, we have limited our tree to five leaf nodes.

The fit() command tells Python to fit the decision tree that was previously specified to the data. The predictor variables are given first, followed by the target variable. Thus, the two inputs to fit() are the X and y objects we created. We save the decision tree as cart01.

Finally, to obtain the tree structure, we use the export_graphviz() command.

```python
export_graphviz(cart01, out_file = "C:/.../cart01.dot",
feature_names=X_names, class_names=y_names)
```

The first input is the decision tree itself, which we saved as cart01. The out_file input will save the tree structure to the specified location and name the file cart01.dot. Run the contents of the file through the graphviz package to display the CART model. Specifying feature_names = X_names and class_names = y_names add the predictor variable names and the target variable values to the cart01 dot file, greatly increasing its readability.

To obtain the classifications of the Income variable for every variable in the training data set, use the predict() command.

```python
predIncomeCART = cart01.predict(X)
```

Using the predict() command on cart01 says that we want to use our CART model to make the classifications. Including the predictor variables X as input specifies that we want to make predictions for those records in particular. The result is the classification, according to our CART model, for every record in the training data set. We save the predictions as predIncomeCART.

### 6.2.2 How to Build CART Decision Trees Using R

Import the training data set and name it adult_tr. Once the data set is loaded into R, rename "Marital status" to "maritalStatus" to remove the space. This change will help our code later.

```r
colnames(adult_tr)[1] <- "maritalStatus"
```

The colnames() command lists the names of each of the variables in the adult_tr data set. Run it on its own, it will output the column names in order. Note that the first column contains the Marital status variable. Using the [1] at the end of colnames(adult_tr) isolates the variable name for Marital status. We then rename the variable by creating the string "maritalStatus" and saving it as the variable's name.

We then change both the categorical variables to factors.

```r
adult_tr$Income <- factor(adult_tr$Income)
adult_tr$maritalStatus <- factor(adult_tr$maritalStatus)
```

To run and visualize the CART model, we need to install and open the required packages, rpart and rpart.plot.

```r
install.packages(c("rpart", "rpart.plot"))
library(rpart) ; library(rpart.plot)
```

Finally, let us run the rpart() command to build the CART model.

```r
cart01 <- rpart(formula = Income ~ maritalStatus + Cap_Gains_Losses,
                data = adult_tr, method = "class")
```

The formula input has the structure Target ~ Predictors, where the names of the predictors are separated by plus signs. The data input specifies which data set the variables are coming from. The method = "class" input specifies that we want to use a classification (CART) model. Finally, we save the resulting model as cart01.

Once the CART model is built, we can plot the CART model with the default display options using the rpart.plot command.

```r
rpart.plot(cart01)
```

The rpart.plot() command takes as its only required input the name under which you saved the CART model. Since we called our model cart01, that is our input.

Note that the plot built using the default settings of rpart.plot() do not replicate Figure 6.1. What other settings are there?

```r
?rpart.plot
```

Run ?rpart.plot to look at the different display options, located under the type and extra arguments. Try using type = 4 to label each branch with its specific value, instead of a yes/no at the top of the split; and extra = 2 to add the correct classification proportion to each node.

```r
rpart.plot(cart01, type = 4, extra = 2)
```

The result is shown in Figure 6.1.

To obtain classifications for each record in the data set using the CART model, you first need to create a data frame that includes the predictor variables of the records you wish to classify.

```r
X = data.frame(maritalStatus = adult_tr$maritalStatus,
               Cap_Gains_Losses =
               adult_tr$Cap_Gains_Losses)
```

The data frame X contains the two predictor variables that were used to build the CART model. It is vitally important that the variable names in this new data frame exactly match the variable names used to build the CART model.

Once you have the predictor variables you wish to classify, use the predict() command.

```r
predIncomeCART = predict(object = cart01, newdata = X,
                         type = "class")
```
