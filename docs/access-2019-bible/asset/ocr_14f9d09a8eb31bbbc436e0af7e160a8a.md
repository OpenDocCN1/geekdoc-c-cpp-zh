# Tip

Think of the commas in an IIf function as THEN and ELSE statements. Consider the following IIf function, for instance:

IIf(Babies = 2 , "Twins", "Not Twins")

This function literally translates to: If Babies equals 2, then Twins, else Not Twins.

# Using IIf to avoid mathematical errors

To demonstrate a simple problem where the IIf function comes in handy, build the query shown in Figure 13.9.

# FIGURE 13.9

This query will perform a calculation on the Actual and the Forecast fields to calculate a percent to forecast.

![](bbox=[0.22, 0.58, 0.72, 0.75])

When you run the query, you'll notice that not all the results are clean. As you can see in Figure 13.10, you're getting some errors due to division by zero. That is, you're dividing actual revenues by forecasts that are zero.

# FIGURE 13.10

The errors shown in the results are due to the fact that some revenues are being divided by zeros.

![](bbox=[0.22, 0.97, 0.48, 1.0])