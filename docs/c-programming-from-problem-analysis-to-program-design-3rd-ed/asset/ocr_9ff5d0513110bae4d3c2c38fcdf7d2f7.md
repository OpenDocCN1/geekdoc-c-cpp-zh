![](bbox=[0.18, 0.09, 0.7, 0.43])

Figure 2-15  Problem specification sheet for the CarpetCalculator example

# Analyze the Problem

You should review the problem specification in Figure 2-15 and make sure you understand the problem definition. No program inputs are included in this solution. After you learn how data can be entered into your program, you will probably want to revise your solution so that you can run your application any number of times with different types and prices of carpeting. For now, the problem does not require you to input values.

However, data is needed in the program. Begin by determining what kinds of data. What types of values (i.e., whole numbers, numbers with a decimal point, Boolean, alphabetic characters, or strings) will be in each of the identified data items? Are there any constant data items? What would be appropriate identifiers for the variables and constants? What is the range of values or domain of the data item? These are all questions that should be asked. The items listed here describe the data needs for this problem:

+   - The dimensions of the room are given in feet and inches—whole numbers and integers—representing both values (i.e., 12 feet 2 inches).
+   - The carpet prices are given as a price per square yard. This value is a number with a decimal portion (i.e., 27.95).
+   - To determine the number of square yards, you must calculate the number of square feet.
+   - Because the width and length are given in feet and inches, you first convert these measurements (feet and inches) into single units for both the width and length.
+   - A memory location is needed to store the total square yards. But, to get that value, a memory location is needed to hold total square feet.
+   - A memory location is needed to hold the total cost of the carpet.