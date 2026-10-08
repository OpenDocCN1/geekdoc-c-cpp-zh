# CHAPTER 4 Completing the Problem-Solving Process

# HOW TO Write an Assignment Statement

Syntax
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
customerName = "Jeff Brown";nThe assignment statement assigns the string "Jeff Brown" to the customerName variable.

Figure 4-11 How to write an assignment statement with a variable declaration

It is easy to confuse an assignment statement in C++. For example, the assignment statement hours = 50; looks very similar to the variable declaration int hours = 50; The noticeable difference is the data type that at the beginning of the declaration statement. However, keep in mind that a variable statement creates (and optionally initializes) a new variable. An assignment statement, on the other hand, assigns a value to an existing variable.

Shaded in Figure 4-12 are the appropriate calculation statements for the Trey Mosble problem. Because all of the items in calculation statements have the same data type, neither statement requires any implicit or explicit type conversions.