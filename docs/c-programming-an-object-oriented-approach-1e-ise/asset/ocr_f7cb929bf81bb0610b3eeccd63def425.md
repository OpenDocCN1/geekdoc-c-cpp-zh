# ### Program 4.1 Printing absolute value

```
```text
1  /************************************************************
2   * Using if-statement to print the absolute value of a number        *
3   ************************************************************/
4  #include <iostream>
5  using namespace std;
6
7  int main ()
8  {
9      // Declaration
10     int number;
11     // Getting input
12     cout << "Enter an integer: ";
13     cin >> number;
14     // Finding the absolute value
15     if (number < 0)
16     {
17         number = -number;
18     }
19     // Printing the absolute value
20     cout << "Absolute value of the number you entered is: " << number;
21     return 0;
22 }

Run:
Enter an integer: 25
Absolute value of the number you entered is: 25

Run:
Enter an integer: -17
Absolute value of the number you entered is: 17
```
```

# ### EXAMPLE 4.1

Program 4.1 shows a very simple use of an if statement to find the absolute value of an integer entered by the user of the program. If the user enters a negative integer, the programs changes it to a positive integer of the same magnitude; otherwise, the program does nothing. After the program exits the decision-making section (lines 15 to 18), it prints the absolute value of the integer entered.

Note that we do not need the braces (lines 16 and 18) in this simple example, but it is a good practice to use them.

# ### EXAMPLE 4.2

Program 4.2 also demonstrates the use of an if statement. It calculates the weekly gross earnings for an employee. If the employee works more than 40 hours during the week, the overtime pay rate for the extra hours is 130 percent of the base pay rate.