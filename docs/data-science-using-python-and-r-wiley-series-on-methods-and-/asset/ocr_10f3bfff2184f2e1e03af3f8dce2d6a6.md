![](bbox=[0.13, 0.08, 0.87, 0.47])

Figure 1.1 Data science methodology: the seven phases.

The data preparation phase is covered in Chapter 3.

# 3. Exploratory Data Analysis Phase.

Now that your data are nice and clean, we can begin to explore the data, and learn some basic information. Graphical exploration is the focus here. Now is not the time for complex algorithms. Rather, we use simple exploratory methods to help us gain some preliminary insights. You might find that you can learn quite a bit just by using these simple methods. Here are some of the ways we can do this.

+   a. Exploring the univariate relationships between predictors and the target variable.
+   b. Exploring multivariate relationships among the variables.
+   c. Binning based on predictive value to enhance our models.
+   d. Deriving new variables based on a combination of existing variables.

We cover the exploratory data analysis phase in Chapter 4.

# 4. Setup Phase.

At this point we are nearly ready to begin modeling the data. We just need to take care of a few important chores first, such as the following:

+   a. Cross-validation, either twofold or n-fold. This is necessary to avoid data dredging. In addition, your data partitions need to be evaluated to ensure that they are indeed random.
+   b. Balancing the data. This enhances the ability of certain algorithms to uncover relationships in the data.