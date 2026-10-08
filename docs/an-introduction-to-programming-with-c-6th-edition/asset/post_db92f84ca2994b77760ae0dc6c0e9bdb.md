
# Assignment Statements

Example 3 firstNum / static_cast<double>(secondNum) (continued)
1. The value stored in the firstNum variable (the integer 2) is explicitly promoted to the double number 2.0.
2. The value stored in the firstNum variable (the integer 5) is implicitly promoted to the double number 5.0.
3. The double 5.0 (the result of Step 2) is divided by the double number 2.0 (the result of Step 1). The result of the division is the number 2.5.

Example 4 IN = 10.65 * static_cast<double>(firstNum)
The value stored in the firstNum variable (the integer 5) is explicitly promoted to the double number 5.0 before being multiplied by the number 10.65. The result is double 53.25. The static_cast operator is not required in this example, because the computer converts the firstNum variable to the double data type before performing the multiplication operation.

Example 5 float PRICE = static_cast<float>(3.99);
The double 3.99 is explicitly converted to the float data type before being stored in the PRICE named constant.

Figure 4-10 How to use the static_cast operator

In most cases, the result of an arithmetic expression is assigned to a variable in a program. You use this an assignment statement.

# Assignment Statements

You can use an assignment statement to assign a value to a variable while a program is running. Figure 4-11 shows the syntax of an assignment statement in C++. The = symbol is syntax called the assignment operator. The figure also includes examples of assignment statements. (For clarity, the variable declaration statements are included in the examples.) An assignment statement tells the computer to evaluate the expression that appears on the right side of the assignment operator and then store the result in the variable named on the left side of the assignment operator. The expression can include one or more items, and the items can be literals, constants, variables, or arithmetic operators. With declarations, the data type of the assignment statement must match the data type of the variable to which the expression is assigned. As you learned in Chapter 3, when a value's data type does not match the memory location's data type, the computer uses a process called implicit conversion to convert the value to fit the memory location. however, if the value does not yield results, it is considered a good programming practice to use a cast, if necessary, to explicitly convert the value to fit the memory location. When a value is assigned to a variable, it replaces the existing value in the memory location; this is because a variable can store only one value at any time.

> You cannot use an assignment statement to assign a value to a named constant because the contents of a named constant cannot be changed during runtime.

# CHAPTER 4 Completing the Problem-Solving Process

# HOW TO Write an Assignment Statement

### Syntax
variableName = expression;

Example 1
int quantity = 0;
quantity = 1000;
The assignment statement assigns the integer 1000 to the quantity variable.

Example 2
int janOrder = 500;
int febOrder = 225;
int total = 0;
total = janOrder + febOrder;
The assignment statement assigns the integer 725 to the total variable.

Example 3
int firstNum = 5;
int secondNum = 2;
double quotient = 0.0;
quotient = static_cast<double>(firstNum) / secondNum;
The assignment statement assigns the double number 2.5 to the quotient variable.

Example 4
char middleInitial = ' ';
middleInitial = 'C';
The assignment statement assigns the letter C to the middleInitial variable.

Example 5
string customerName = "";
customerName = "Jeff Brown";
The assignment statement assigns the string "Jeff Brown" to the customerName variable.

Figure 4-11 How to write an assignment statement with a variable declaration

It is easy to confuse an assignment statement in C++. For example, the assignment statement hours = 50; looks very similar to the variable declaration int hours = 50; The noticeable difference is the data type that at the beginning of the declaration statement. However, keep in mind that a variable statement creates (and optionally initializes) a new variable. An assignment statement, on the other hand, assigns a value to an existing variable.

Shaded in Figure 4-12 are the appropriate calculation statements for the Trey Mosble problem. Because all of the items in calculation statements have the same data type, neither statement requires any implicit or explicit type conversions.

# Assignment Statements

| IPO chart information | C++ instructions |
| --- | --- |
| Input | double totalBill = 0.0; |
| total bill | double liquor = 0.0; |
| liquor charge | double tipPercent = 0.0; |
| tip percentage | |
| Processing | |
| total bill without liquor charge | double totalLiquor = 0.0; |
| Output | |
| tip | double tip = 0.0; |
| Algorithm | |
| 1. enter the total bill, liquor charge, and tip percentage | cout << "Enter the total bill: ";\n >> totalBill;\nout << "Enter the liquor charge: ";\n >> liquor;\nout << "Enter the tip percentage in decimal format: ";\nout >> tipPercent; |
| 2. calculate the total bill without liquor charge by subtracting the liquor charge from the total bill | totalLiquor = totalBill - liquor; |
| 3. calculate the tip by multiplying the total bill without liquor charge by the tip percentage | tip = totalLiquor * tipPercent; |
| 4. display the tip | cout << "Tip: " << tip << endl; |

Figure 4-12 Calculation statements for the Treyson problem

You have coded the algorithm into a program, which is Step 4 in the problem-solving process. Before moving on Step 5, it is important to caution you about a problem you might encounter when using real numbers in calculations. As mentioned in Chapter 3, not all real numbers can be represented exactly with the computer's internal memory. As a result, the answer to calculations may not be accurate to the penny. For example, the expression 7 / 3.0 yields 2.333333... (with the number 3 repeating indefinitely). The number 2.333333... can be stored in the computer's memory only with approximation. Because many real numbers cannot be stored precisely, some programmers do not use integers in monetary calculations where accuracy to the penny is required. Instead, some programmers use integers, while others use special classes to perform precise arithmetic using real numbers. These special classes can be purchased from third-party vendors, such as Rogue Software. You can learn more about the problem of using real numbers in monetary calculations by completing Exercise 15 at the end of this chapter. The exercise also allows you to explore the use of integers in calculations. (Your instructor may require you to use integers in monetary calculations; however, for simplicity, this book will use real numbers.)

# CHAPTER 4

# Completing the Problem-Solving Process

The answers to Mini-Quiz questions are located in Appendix A.

# Mini-Quiz 4-2

- 1. Write a C++ assignment statement that multiplies the number 9.55 by the value stored in an int named hours and then assigns the result to a double named grossPay. Use implicit type conversion.
- 2. Rewrite the answer to Question 1 using a type cast (explicit type conversion).
- 3. In C++, the expression 7 / 2 * 4.5 will evaluate to when it should evaluate to Why does the expression evaluate incorrectly?
- 4. Rewrite the expression from Question 3 so that it will evaluate correctly.

# Step 5—Desk-check the Program

The fifth step in the problem-solving process is to desk-check the program to make sure that each instruction in the algorithm was translated correctly. You should desk-check the program using the same sample data used to desk-check the algorithm; results of both desk-checks should be the same. For convenience when comparing the results of both-checks later in this section, Figure 4-13 shows the desk-check table you completed for the Treysonley algorithm in Chapter 2.

| total bill liquor charge | tip percentage total bill without liquor charge | tip |
|---|---|---|---|---||
| 45 | 10 | | 35 | |
| 30 | 0 | 15 | 30 | 4.5 |

**Figure 4-13** Algorithm's desk-check table from Chapter 2

When checking a program, you first place the names of the memory locations (variables and named constants) in a new desk-check table, along with each memory location's initial value. Figure 4-14 shows the result of desk-checking the variable declaration statements earlier in Figure 4-12.

| totalBill | liquor | tipPercent | totalLiquor | tip |
|---|---|---|---|---||
| 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |

**Figure 4-14** Variable names and initial values entered in the program's desk-check table

Next, you desk-check the remaining C++ instructions in order, recording in the desk-check table any changes made to the variables. In the Treyson Mosley program, the first instruction following the declaration statements
