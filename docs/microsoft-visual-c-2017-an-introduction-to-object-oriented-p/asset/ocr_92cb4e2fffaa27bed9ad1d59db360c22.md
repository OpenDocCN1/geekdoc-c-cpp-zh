20. Suppose that you have declared an integer named scores, and you make the following method call:
TotalScores(scores, num : 1);
Of the overloaded method definitions, which would execute?

+   a. private static void TotalScores(int[] scores)

+   b. private static void TotalScores(int[] scores, int num)

+   c. private static void TotalScores(int[] scores, int num = 10,
int code = 10)

+   d. The program would not compile.

# Exercises

Programming Exercises

+   a. Create a program named Reverse3 whose Main() method declares three integers firstInt, middleInt, and lastInt. Assign values to the variables, display them, and then pass them to a method that accepts them as reference variables, place the first value in the lastInt variable, and place the last value in the firstInt variable. In the Main() method, display the three variables again, demonstrating that their positions have been reversed.

+   b. Create a program named Reverse4, which contains a method that reverses the positions of four values. Write a Main() method that demonstrates the method works correctly.

+   2. Create a program named IntegerFacts whose Main() method declares an array of 10 integers. Call a method to interact fill the array with any number of values up to 10 until a sentinel value is entered. If an entry is not an integer, prompt the user. Call a second method that outputs parameters for the highest value in the array, lowest value in the array, sum of the values in the array, and arithmetic mean. In the Main() method, display all statistics.

+   3. Create a program for Smalltown Regional Airport Flights that accepts either an integer number or string code from the options in Figure 8-33. Pass the

| Flight number | Airport code | Airport name | Time |
|---|---|---|--|
| 201 | AUS | Austin | 0710 |
| 321 | CRP | Corpus Christi | 0830 |
| 510 | DFW | Dallas Fort Worth | 0915 |
| 633 | HOU | Houston | 1140 |

Figure 8-33 Flight information for Smalltown Regional Airport