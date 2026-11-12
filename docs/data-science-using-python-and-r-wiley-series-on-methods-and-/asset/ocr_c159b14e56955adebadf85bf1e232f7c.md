# 6.1 INTRODUCTION TO DECISION TREES

Thus far, we have become acquainted with the first four phases of the Data Science Methodology:

+   1. Data Understanding Phase
+   2. Data Preparation Phase
+   3. Exploratory Data Analysis Phase
+   4. Setup Phase.

We are ready to finally begin modeling our data, in the Modeling Phase. Data science offers a wide variety of methods and algorithms for modeling large data sets. We begin here with one of the simplest methods: decision trees. In this chapter we will work with the adult_ch6_training and the adult_ch6_test data sets. These are adapted from the Adult data set from the UCI repository. For simplicity, only two predictors and the target are retained, as follows:

+   * Marital status, a categorical predictor with classes married, divorced, never-married, separated, and widowed.
+   * Cap_gains_losses, a numerical predictor, equal to capital gains + capital losses.
+   * Income, a categorical target variable with two classes, >50k and ≤50k, representing individuals whose income is greater than $50,000 per year, and those with income less than or equal to $50,000 per year.

A decision tree consists of a set of decision nodes, connected by branches, extending downward from the root node until terminating in leaf nodes. Beginning at the top node, which by convention is placed at the top of the decision tree

> 'C.L. Blake and C.J. Merz, UCI Repository of Machine Learning Databases, Department of Information and Computer Science, University of California, Irvine, CA, 1998 Adult data set donated by Ron Kohavi.