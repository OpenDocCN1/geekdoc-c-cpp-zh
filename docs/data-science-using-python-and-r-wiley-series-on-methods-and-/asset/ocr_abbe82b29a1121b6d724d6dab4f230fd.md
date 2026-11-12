value of x produce moderate increments in the value of f(x); however, near the extremes, moderate increments in the value of x produce tiny increments in the value of f(x).

# ## 9.5 BACKPROPAGATION

How does the neural network learn? As each observation from the training set is processed through the network, an output value is produced from the output node. This output value is then compared to the actual value of the target variable for this training set observation and the error (actual – output) is calculated. This prediction error is analogous to the prediction error in linear regression models. To measure how well the output predictions fit the actual target values, most neural network models use the sum of squared errors (SSE):

SSE = \sum_{records} \sum_{output nodes} (actual - output)^2

where the squared prediction errors are summed over all the output nodes and over all the records in the training set. The problem is therefore to *construct a set of model weights that will minimize the SSE*. In this way, the weights are analogous to the parameters of a regression model. The “true” values for the weights that will minimize SSE are unknown and our task is to estimate them, given the data.

However, due to the nonlinear nature of the sigmoid functions permeating the network, there exists no closed-form solution for minimizing SSE as exists for least-squares regression. Optimization methods, specifically gradient-descent methods, are thereafter used.

The backpropagation algorithm does the following:

+   1. It takes the prediction error (actual – output) for a particular record and percolates the error back through the network.
+   2. Assigning partitioned responsibility for the error to the various connections.
+   3. The weights on these connections are then adjusted to decrease the error, using gradient descent.¹

# ## 9.6 AN APPLICATION OF A NEURAL NETWORK MODEL

We next turn to an example of a neural network model using a subset of the Framingham Heart Study data.² The data set, *Framingham_training*, contains information on three variables for 7953 patients. *Sex* is a binary predictor with