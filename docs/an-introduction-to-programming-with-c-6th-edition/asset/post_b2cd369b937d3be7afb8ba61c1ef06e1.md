
# CHAPTER 9 Value-Returning Functions

(continued)

| getBonus function | C++ instructions |
|---|---|
| IPO chart information | int sold |
| Input | double bonusRate |
| sales (formal parameter) | |
| bonus rate (formal parameter) | |

# Processing

none

# Output

bonus = doubleBonusAmt = 0.0;

# Algorithm

+   1. calculate the bonus by multiplying the sales by the bonus rate
2. return the bonus

bonusAmt = sold * bonusRate;

return bonusAmt;

Figure 9-29 IPO chart and C++ code for the getBonus function

The C++ code for the entire program is shown in Figure 9-30. The function calls appear on Lines 19 and 20 in the main function and are shaded in the figure. The function definitions are located below the main function, on Lines 31 through 44. The function prototypes are located above the main function, on Lines 9 and 10. Figure 9-31 shows a sample run of the bonus calculator program.

```cpp
// Calculator.cpp - displays the amount of a bonus
23 //Created/revised by <your name> on <current date>
4 #include <iostream>
5 #include <iomanip>
6 using namespace std;
7
8 // function prototypes
9 int getSales();
10 double getBonus(int sold, double bonusRate);
11
12 int main()
13 {
14 int sales = 0;
15 double bonus = 0.0;
16
17
18 //call functions to get the sales and
19 //calculate the bonus
20 sales = getSales();
21 bonus = getBonus(sales, .05);
22
23
24 //display the bonus
25 cout << fixed << setprecision(2);
```

Figure 9-30 Bonus calculator program (continues)

# The Scope and Lifetime of a Variable

| | |
|---|---|
| 24 | cout << "Bonus: $" << bonus << endl; |
| 25 | |
| 26 | system("pause"); | your C++ development tool may not require this statement |
| 27 | return 0; |
| 28 | //end of main function |
| 29 | |
| 30 | //****function definitions**** |
| 31 | int getSales() |
| 32 | { |
| 33 | int salesAmt = 0; |
| 34 | cout << "Enter sales: "; |
| 35 | cin >> salesAmt; |
| 36 | return salesAmt; |
| 37 | } //end of getSales function |
| 38 | |
| 39 | double getBonus(int sold, double bonusRate) |
| 40 | { |
| 41 | double bonus = 0.0; |
| 42 | bonus = sold * bonusRate; |
| 43 | return bonus; |
| 44 | } //end of getBonus function |

Figure 9-30 Bonus calculator program

![](img/d64a28a68f49d61137bf2f3170ac40ad_363_0)

Figure 9-31 Sample run of the bonus calculator program

Desk-check the program in Figure 9-30 using 1575 as the sales amount. The statements on Lines 14 and 15 initialize an int sales and a double bonus. Both variables are local to the main function, which means they can be used only within that function. Both variables remain in the computer's internal memory until the main function ends. Figure 9-32 shows the desk-check table after the variable declaration statements on Lines 14 and 15 are processed.

![](img/d64a28a68f49d61137bf2f3170ac40ad_363_1)

Figure 9-32 Desk-check table after the variable declaration statements on Lines 14 and 15 are processed

# Value-Returning Functions

When the computer encounters the `sales = getSales();` statement on Line 19, it temporarily leaves the main function to process the getSales function's code, beginning with the function header on Line 31. The function header does not contain any parameters, which indicates that the function will not receive any information when it is called. The first statement in the getSales body creates an int variable named salesAmt. The variable is local to the getSales function, which means it can be used only within that function. The salesAmt variable will remain in the computer's internal memory until the getSales function ends. The next statements in the getSales function prompt the user to enter a sales amount and then store the user's response—in this case 1575—in the salesAmt variable. Figure 9-33 shows the sales amount entered in the desk-table.

| main function's variables | | getSales function's variable |
|---|---|---|
| sales | bonus | salesAmt |
| | 0.0 | 1575 |

Figure 9-33 Desk-table after the sales amount entered

Next, the computer processes the getSales function's return statement, which returns the salesAmt variable's value to the statement that called it. In fact, it returns the value to the assignment statement on Line 19 in the main function. The statement assigns the return value to the sales variable, as shown in Figure 9-34.

| main function's variables | | getSales function's variable |
|---|---|---|
| sales | bonus | salesAmt |
| | 0.0 | 1575 |

Figure 9-34 Desk-table after the sales amount is returned to the main function

After its return statement is processed, the getSales function ends and the computer removes the salesAmt variable from memory. Figure 9-35 shows the desk-table after the getSales function ends. Only the main function's variables are still in memory.

| main function's variables | | getSales function's variable no longer exists in the computer's memory |
|---|---|---|
| sales | bonus | |
| | 0.0 | |

Figure 9-35 Desk-table after the getSales function ends

# The Scope and Lifetime of a Variable

Next, the computer processes the `bonus = getBonus(sales, .05);` statement on Line 20 in the main function. The statement calls the getBonus function, passing it two arguments. Here the computer leaves the main function. However, in this case, it does so to process the code in the getBonus function, beginning the function header. The two parameters in the parameter list tell the computer to create an int named sold and a double named bonusRate. The variables are local to the getBonus function and can be used only within that function. The computer stores the first value passed to the function's first parameter, and it stores the second value passed to the function's second parameter. In this case, it stores the sales variable's value in the sold variable and the bonusRate variable, as shown in Figure 9-36.

![](img/d64a28a68f49d61137bf2f3170ac40ad_365_0)

Figure 9-36 Desk-check after the getBonus function header is processed

The first statement in the getBonus function declares an additional local variable: double bonus named bonus. The second statement multiplies the contents of the sold variable by the contents of the bonusRate and assigns the result (78.75) to bonus bonus, as shown in the desk-check table indicates that two locations in the computer's memory have the same name: bonus. When the bonus appears in a statement, the computer uses the position of the statement to determine which of the two locations to use. If the program appears in the main function, the computer uses the bonus variable located in the main function's memory. However, if the program appears in the getBonus function, the computer uses the bonus variable located in the getBonus function's memory.

![](img/d64a28a68f49d61137bf2f3170ac40ad_365_1)

Figure 9-37 Desk-check after the bonus function is calculated

Next, the computer processes the getBonus function's return statement.

# Value-Returning Functions

The statement returns the value stored in the function's bonus variable to the statement that called it. In this case, it returns the value to the assignment on Line 20 in the main function. The statement assigns the return value to the sales variable, as shown in Figure 9-38. At this point, the getBonus function ends and the computer removes the local variables (sold, bonusRate, and bonus) from memory. Figure 9-38 shows the desk-check table after the getBonus function ends.

| main function's variables | | salesAmt | sold | bonusRate | bonus |
|---|---|---|---|---|---|
| sales | bonus | | | | |
| | 0.0 | | 1575 | 05 | 75.75 |

Figure 9-38 Desk-check table after the getBonus function ends

After the getBonus function ends, the computer processes the remaining instructions in the main function. The cout statements on Lines 23 and 24 display the bonus in fixed-point notation with two decimal places. The system("pause");"); statement on Line 26 pauses program execution, and the return 0; statement on Line 27 returns the number 0 to the operating system. After the return 0; statement is processed, the program ends and the computer removes the main function's variables (sales and bonus) from memory.

The answers to Mini-Quiz questions are located in Appendix A.

# Mini-Quiz 9-4

+   1. A variable's lifetime indicates the portions of a program that can use the variable.
   a. True
   b. False
2. Unless specified otherwise, variables in C++ are passed by contents.
   a. True
   b. False
3. The variables in a function header have local scope.
   a. True
   b. False
4. Two functions in a program declare a variable using the same name. How does the computer know which variable to use?
