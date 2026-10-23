Parameter lists the names of the model parameters. To the right of the list of parameters are columns of zeros corresponding to these parameters. Click in these cells to enter a new hypothesized parameter value corresponding to the desired test.

One of the parameters is labeled “ = ”. In the edit box to its right, enter the value that you are testing the contrast against. For example, you may be testing that a certain combination of the factors sums to 1. You would enter a 1 beside the “ = ” in this dialog.

Add Column adds another column of zeros so that several linear functions of the parameters can be jointly tested. Use the Add Column button to add as many columns to the test as needed.

When the test is specified, click Done to see the test performed. The results are appended to the bottom of the dialog.

When the custom test is done, the report lists the test name, the function value of the parameters tested, the standard error, and other statistics for each test column in the dialog. A joint F test for all columns is at the bottom. Sample output for a custom test (that the Size of Load coefficient is equal to 1) is shown in Figure 5.14.

# Figure 5.14 Custom Test Output

![](bbox=[0.41, 0.4, 0.65, 0.69])

Note: For tests within a categorical effect, instead of using a Custom test, consider using the contrast dialog, which tests hypotheses about the least squares means.

# Correlation of Estimates

The Correlation of Estimates option in the Estimates platform menu produces a correlation matrix for the all effects in a model.

# Row Diagnostics

Leverage Plots (the Plot Actual by Predicted and Plot Effect Leverage commands) are covered previously in this chapter under “Leverage Plots,” p. 91.