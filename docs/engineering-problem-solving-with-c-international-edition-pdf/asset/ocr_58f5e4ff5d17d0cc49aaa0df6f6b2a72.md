# Modify!

These problems relate to the program developed in this section for computing new freezing points with linear interpolation.

+   1. Use the program to determine the freezing temperatures to go with the following salinity measurements in ppt:
+   3 8.5 19 23.5 26.8 30.5
+   
+   2. Modify the program so that it converts and prints the new temperature in degrees Centigrade. (Recall that T_F = 9/5 T_C + 32, where T_F represents a temperature in degrees Fahrenheit and T_C represents a temperature in degrees Centigrade.)
+   
+   3. Suppose that the data used with the program contained values with the degrees in Centigrade. Would the program need to be changed? Explain.
+   
+   4. Modify the program so that it interpolates for a salinity, instead of a new freezing temperature. (You may want to refer to Figure 3.12, which contains a plot of this data with the freezing temperature on the x axis and the salinity on the y axis.)

![](bbox=[0.23, 0.46, 0.88, 0.66])

Figure 3.12 Salinity at the freezing temperature of seawater.

# 3.7 Selection Statements: switch Statement

The switch statement is used for multiple-selection decision making. In particular, it is often used to replace nested if/else statements. Before giving the general discussion of the switch statement, we present a simple example that uses nested if/else statements and then an equivalent solution that uses the switch statement.

Suppose that we have a temperature reading from a sensor inside a large piece of machinery. We want to print a message on the control screen to inform the operator of the temperature status. If the status code is 10, the temperature is too hot, and the equipment should be turned off; if the status code is 11, the operator should check the temperature every