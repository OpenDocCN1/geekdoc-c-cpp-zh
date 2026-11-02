These graphs offer a quick view of the distribution of each independent variable in relation to LOAN_DEFAULT. The variable is also highly skewed to the right. In subsequent steps, you will scrub the tot_bal_open_Accounts variable for outliers and transform it to make it more normally distributed.

# Modify

This section illustrates how to prepare the data for modeling. You will impute values to replace missing values, partition the data, filter outliers, and transform the independent variables.

# Replace Missing Values via Imputation

The next step is to impute values for missing or incorrect observations. Recall that the StatExplore window revealed that the Marital Status and Income variables have missing values.

Begin by clicking **Modify** and dragging the **Impute** icon onto the diagram, as shown in Figure 9.9.

**Figure 9.9: Impute Missing Values**

![](bbox=[0.115, 0.434, 0.473, 0.619])

The Property window is populated with default methods for imputing missing values. The class variables are replaced with the value that has the highest count. The highest count value is used as a replacement for Marital Status. Recall that Gender has a value U for *unknown*. You can leave this value as is: Sometimes the fact that the Gender is unknown is predictive. If it were missing, it would be set to M because of a higher count of customers with Gender = M.

For interval variables, the default method is to replace missing values with the mean value. Because your number of missing values is small, this default is adequate. If it were a larger percentage, then using a more advanced method, such as tree, might be better. To learn more about the Tree Imputation Method, see Contents in the Help section of Enterprise Miner.

Right-click on the **Impute** icon and click **Run ▶ Yes**. When complete, click **Results**. Output 9.5 shows a partial view of the number of imputed values as well as the value used to replace the missing values.