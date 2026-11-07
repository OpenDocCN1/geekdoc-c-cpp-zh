8. The Programming Example, Converting a Number from Decimal to Binary, in Chapter 15, contains a program that uses recursion to convert a decimal number into an equivalent binary number. Write a program that uses a stack to convert a decimal number into an equivalent binary number.

9. Write a program that reads a string consisting of a positive integer or a positive decimal number and converts the number to the numeric format. If the string consists of a decimal number, the program must use a stack to convert the decimal number to the numeric format.

10. **(Infix to Postfix)** Write a program that converts an infix expression into an equivalent postfix expression.

The rules to convert an infix expression into an equivalent postfix expression are as follows:

Suppose **infx** represents the infix expression and **pfx** represents the postfix expression. The rules to convert **infx** into **pfx** are as follows:

+   a. Initialize **pfx** to an empty expression and also initialize the stack.
+   
+   b. Get the next symbol, **sym**, from **infx**.
+   
+   &nbsp;&nbsp;&nbsp;&nbsp;b.1. If **sym** is an operand, append **sym** to **pfx**.
+   
+   &nbsp;&nbsp;&nbsp;&nbsp;b.2. If **sym** is (, push **sym** into the stack.
+   
+   &nbsp;&nbsp;&nbsp;&nbsp;b.3. If **sym** is ), pop and append all of the symbols from the stack until the most recent left parentheses. Pop and discard the left parentheses.
+   
+   &nbsp;&nbsp;&nbsp;&nbsp;b.4. If **sym** is an operator:
+   
+   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;b.4.1. Pop and append all of the operators from the stack to **pfx** that are above the most recent left parentheses and have precedence greater than or equal to **sym**.
+   
+   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;b.4.2. Push **sym** onto the stack.
+   
+   c. After processing **infx**, some operators might be left in the stack. Pop and append to **pfx** everything from the stack.

In this program, you will consider the following (binary) arithmetic operators: +, -, *, and /. You may assume that the expressions you will process are error free.

Design a class that stores the infix and postfix strings. The class must include the following operations:

+   - **getInfix**: Stores the infix expression.
+   - **showInfix**: Outputs the infix expression.
+   - **showPostfix**: Outputs the postfix expression.