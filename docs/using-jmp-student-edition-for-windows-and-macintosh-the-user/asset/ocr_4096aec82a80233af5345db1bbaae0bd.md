information on modeling types is found in “The Modeling Type of Variables,” p. 29. Initially, this example consists of three analyses, with Starch Content (%) as the Y variable in all of them. Method, Size of Load (lbs), and Sand Blasted? are the X variables. All three analyses are requested at the same time to illustrate some of JMP Student Edition’s interactive capabilities. These analyses would be equally valid if performed separately.

+   - Select Starch Content (%) from the list of columns and click the Y, Response button.
+   - To select all three X variables, click on Method, hold down the Shift key, then click Sand Blasted?.
+   Note that these dialog boxes respond to dragging as well as button clicks, as in the next step.
+   - Drag these highlighted variables to the box to the right of the X, Factor button.
+   - Click OK.

Three plots appear as in Figure 3.2.

# Figure 3.2 Fit Y by X Results

![](bbox=[0.17, 0.35, 0.83, 0.49])

On the far left and far right, dot plots of each level of a nominal variable are plotted side by side, a situation leading to one-way ANOVAs. In the middle plot, JMP Student Edition produces a scatterplot of two continuous variables, a situation leading to fitting lines and curves.

# Computing a t-test

As a simple example, examine the plot on the far right, relating starch content to whether the fabric was sand blasted or not. Is the starch content different for the two levels of Sand Blasted? This is a typical situation examined with a two-sample t-test. To conduct the t-test,

+   - Select t test from the drop-down menu in the plot’s title bar.

The t-test report appears in the outline beneath the plot labeled t test.

# Figure 3.3 t-test Results

![](bbox=[0.27, 0.79, 0.72, 0.89])

Some things should be noticed about this report.