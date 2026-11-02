
Figure 3.8 shows a relationship between *response* (0/1) and *prospect's age*. The goal is to predict the probability of response to a catalog that sells high-end gifts using the *prospect's age*. Notice how the data points have a value of 0 or 1 for *response*. On the *prospect's age* axis, the values of 0 for *response* are clustered around the lower values for *prospect's age*. Conversely, the values of 1 for *response* are clustered around the higher values for *prospect's age*. A sigmoidal function, or S curve, is formed by averaging the 0s and 1s for each value of *prospect's age*. You can see that older prospects respond at a higher rate than younger prospects.

**Figure 3.8: Example of Simple Logistic Regression of Response (1 = Yes, 0 = No) to Sales Catalog on Prospect's Age (Years)**

![](img/976d9b992e82c4ac7d195d03a30b4915_52_0.png)

The following steps detail the construction of the logit function in simple language. This logistic regression example does not duplicate the data represented in the above graph, but it conveys the general idea:

- 1. For each value of *prospect's age*, calculate a probability (*p*) by averaging the values of response.
- 2. For each value of *prospect's age*, calculate the odds by using the formula *p*/(1 − *p*).
- 3. The final transformation calculates the log of the odds: log (*p*/(1 − *p*)).
- 4. The parameter estimates are derived using maximum likelihood estimation, which produces the parameter estimates that are most likely to occur given the data. The parameter estimates are related to the log of the odds as follows: log (*p*/(1 − *p*)) = β0 + β1X1 + β2X2 + ... + βnXn, where β0 ... βn are the parameter estimates and X1 ... Xn are the predictive variables.
- 5. After the parameter estimates, also called coefficients or weights (βs), are derived, the final probability is calculated using the following formula: P = exp(β0 + β1X1 + β2X2 + ... + βnXn)/(1 + exp(β0 + β1X1 + β2X2 + ... + βnXn)). This formula is also written in a simpler form as follows: *p* = 1/(1 + exp(−(β0 + β1X1 + β2X2 + ... + βnXn))).
- 6. The process starts with a given value for response at each value of age. Values for *p* are bounded by 0 and 1. Using a link function, you derive a model using maximum likelihood. The result is log (*p* / (1 − *p*)) = 1.233 + 6.39 × *prospect's age* and *p* = 1/(1 + e^(−(1.233 + 6.39 × *prospect's age*))).

The formula enables you to estimate the response rate, given the value for prospect's age.

This example is a simple one; logistic regression models typically have numerous predictive variables.

## Neural Networks

Neural network processing differs greatly from regression in that the process does not follow any statistical distribution. Instead, a neural network is modeled after the function of the human brain. The process is one of pattern recognition and error minimization. You can think of it as ingesting information and learning from each experience.

Neural networks are made up of nodes that are arranged in layers. This construction varies, depending on the type and complexity of the neural network. Figure 3.9 illustrates a simple neural network with one hidden layer. Before the process begins, the data is split into *training* and *testing* data sets. (A third group is sometimes held out for final validation.) Then weights or “inputs” are assigned to each of the nodes in the first layer. During each iteration, the inputs are processed through the system and compared with the actual value. The error is measured and fed back through the system to adjust the weights. In most cases, the weights improve in their ability to predict the actual values. The process ends when a predetermined minimum error level is reached.

**Figure 3.9: Neural Network Schema Showing Flow of Data**

![](img/976d9b992e82c4ac7d195d03a30b4915_54_0.png)

One specific type of neural network commonly used in marketing uses sigmoidal functions to fit each node. Recall that the sigmoidal function is the same function used in logistic regression. You might think about this type of neural network as a series of "nested" logistic regressions. This technique is powerful in fitting a binary, or two-level, outcome, such as a response to an offer or a default on a loan.

One of the advantages of a neural network is its ability to pick up nonlinear relationships in the data. This ability to pick up nonlinear relationships allows users to fit some types of data that would be difficult to fit by using regression. One drawback, however, is its tendency to overfit the data. Overfitting can cause the model to deteriorate more quickly when applied to new data. If this is the method of choice, be sure to carefully validate your data. Another disadvantage to consider is that the results of a neural network are often difficult to interpret.

## Modeling Process

The modeling process has four main stages:

- 1. Define the objective.
- 2. Develop the model.
- 3. Implement the model.
- 4. Track and monitor the model.

### Define the Objective

Defining the objective is the main theme of Chapter 1 because it is the most important step in the model building process. You can develop a perfect model using perfect data. But if it doesn't meet your business objective, it is a waste of time and money. Make sure the objective of the model is in alignment with your overall business goals.

### Develop the Model

The model development process comprises five steps.

- 1. Select the data.
- 2. Explore the data.
- 3. Modify the data and variables.
- 4. Build the model.
- 5. Assess the model.

If you follow this sequence, you will likely be successful in your model-building efforts.

### Step 1: Select the Data

Once you have defined your objective, you need to get data for developing your model. Be sure it correlates with the business purpose for building the model. The data can come from a variety of sources. In some cases, data will need to be combined. The specific details of the data selection are highly specific to the project. To learn about many sources for data construction, see Chapter 4.

### Step 2: Explore the Data

Once your data is available for analysis, you can use visual tools to view the distribution and completeness of the data. Several tables and graphs can display the data values and show you where data is incomplete or missing.

### Step 3: Modify the Data and Variables

In this step, you can partition your data into training, test, and validation data sets. On the basis of your findings in your data exploration step, you can impute missing values and filter outliers.

To ensure the best fit for regression and neural network models, you may want to transform or segment continuous variables. To use class variables in a regression or neural network model, you need to make them numeric. The best way to do so is to create indicator variables for any variables with character or non-numerical values. For an example of this technique, see Chapter 9.

For continuous variables, you can select certain transformations to provide a better fit for your model. SAS Enterprise Miner gives you the option of letting the software pick the best transformation, as is demonstrated in Chapter 9. For more detail on variable transformations, see *Data Mining Cookbook* (Parr-Rud 2001, 85–97).

### Step 4: Build the Model

The process of building the model is greatly streamlined within SAS Enterprise Miner. But it is still good to understand the underlying processes so that you are well prepared to uncover anomalies and errors.

### Selection Method

Earlier in the chapter, you learned about three modeling techniques: decision tree, regression, and neural networks. Each of these techniques offers unique considerations when you are determining your selection method.

For the decision tree model, the variables are split into discrete groups; therefore, you don't have to do any variable transformations or define a selection process. You can interactively build a tree if you are looking to select the variables that you want to enter the model. For information about building a tree interactively, see *Decision Trees for Analytics Using SAS Enterprise Miner* (DeVille and Neville 2013).

The order in which the variables are selected may affect the final outcome of the model. Many selection methods exist. Each one has its advantages and disadvantages. Depending on your particular business problem or resource situation, one method might be preferred over another.

For more detail on selection options for regression, see *Data Mining Cookbook* (Parr-Rud 2001, 104–105).

### Optimal Number of Variables

A common question in relation to the model-building process is, what is the optimal number of variables?

The answer depends on the situation. Most models that predict well have 7 to 15 variables. In certain situations, using every variable might be optimal. Although the model might be large and difficult to interpret, the extra variables do not detract from the power or fit of the model. In some businesses where analytic resources are scarce and CPU power is abundant, using every variable is often the best option.
