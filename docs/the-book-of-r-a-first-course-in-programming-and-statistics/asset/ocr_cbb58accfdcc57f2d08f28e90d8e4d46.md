# Exercise 20.1

Continue to use the survey data frame from the package MASS5 for the
ext few exercises.

+   a. Using your fitted model of student height on writing handspan,
surf, provide point estimates and 99 percent confidence
intervals for the mean student height for handspans of 12, 15.2,
17, and 19.9 cm.

+   b. In Section 20.1, you defined the incomplete.obs, a numeric
vector that provides the records of survey that are automati-
removed from consideration when estimating the model
parameters. Now, use the incomplete.obs vector along with survey
and Equation (20.3) to calculate $\hat{eta}_0$ and $\hat{eta}_1$ in R. (Remember
height, sd, and co. Ensure your answers match the
out from surfit.

+   c. The survey data frame has a number of other variables
aside from Height and wr.H. For this exercise, the end aim is
to fit a simple linear model to predict the mean student height,
with this pulse rate, given in Pulse (continue to
assume the conditions listed in Section 20.2 are satisfied).

+   i. Fit the regression model and produce a scatterplot with the
fitted line superimposed upon the data. Make sure you can
write down the fitted model equation and keep the plot
open.

+   ii. Identify and interpret the point estimate of the slope, as well
as the outcome of the test associated with the hypotheses
H$_0: \beta_1 = 0$; H$_\{A}: \beta_1 \neq 0$. Also find a 90 percent CI for the
slope parameter.

+   iii. Using your model, add lines for 90 percent confidence and
prediction interval bands on the plot from (i) and add a
legend to differentiate between the lines.

+   iv. Create an incomplete.obs vector for the current “height on
pulse” data. Use that vector to calculate the sample mean of
the height observations that were used for the model fitted
in (i). Add a perfectly horizontal line to the plot at this
mean (use color or line type options to avoid confusion with
the other lines present). What do you notice? Does the plot
support your conclusions from (ii)?