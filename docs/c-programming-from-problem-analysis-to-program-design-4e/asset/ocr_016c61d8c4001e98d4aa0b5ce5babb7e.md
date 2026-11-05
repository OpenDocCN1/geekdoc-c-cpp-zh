As you examine Example 5-9, note a call to a method in the Convert class. In Chapter 3, you were introduced to the Parse( ) method to convert values stored in string variables into numeric types. You can also use the Convert class for this conversion. Convert is in the System namespace and has methods for converting one base type into another base type. The Convert.ToDecimal( ) method was used in Example 5-9 to change the inputted string value into a decimal value. To convert to an integer, use Convert.ToInt32( ), and to convert to a double, use Convert.ToDouble( ). If you are using Visual Studio, make sure to use the IntelliSense feature. You can explore the many methods and their overloads available in the Convert class.

For Example 5-9, the output produced when the user enters 600000 is shown in Figure 5-2.

![](bbox=[0.22, 0.45, 0.88, 0.67])

FIGURE 5-2 BonusApp with salesForYear equal to 600000.00

The problem definition indicates that sales must be over $500,000.00 before a bonus is awarded. The output produced when 500000.00 is entered is shown in Figure 5-3.

![](bbox=[0.22, 0.86, 0.88, 0.96])

FIGURE 5-3 BonusApp with salesForYear equal to 500000.00