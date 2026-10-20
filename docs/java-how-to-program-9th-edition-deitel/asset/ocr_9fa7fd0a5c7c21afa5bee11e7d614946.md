# 22.13 (Postfix Evaluator) Write class PostfixEvaluator that evaluates a postfix expression such as 6 2 + 5 * 8 4 / -

The program should read a postfix expression consisting of digits and operators into a StringBuffer. Using modified versions of the stack methods implemented earlier in this chapter, the program should scan the expression and evaluate it (assume it’s valid). The algorithm is as follows:

+   a) Append a right parenthesis ‘)’ to the end of the postfix expression. When the right-parenthesis character is encountered, no further processing is necessary.
+   b) Until the right parenthesis is encountered, read the expression from left to right.
+   If the current character is a digit, do the following:
+   Push its integer value onto the stack (the integer value of a digit character is its value in the Unicode character set minus the value of ‘0’ in Unicode).
+   Otherwise, if the current character is an operator:
+   Pop the two top elements of the stack into variables x and y.
+   Calculate y operator x.
+   Push the result of the calculation onto the stack.
+   c) When the right parenthesis is encountered in the expression, pop the top value of the stack. This is the result of the postfix expression.

[Note: In b) above (based on the sample expression at the beginning of this exercise), if the operator is ‘/’, the top of the stack is 4 and the next element in the stack is 40, then pop 4 into x, pop 40 into y, evaluate 40 / 4 and push the result, 10, back on the stack. This note also applies to operator ‘-’. ] The arithmetic operations allowed in an expression are: + (addition), - (subtraction), * (multiplication), / (division), ^ (exponentiation) and % (remainder).

The stack should be maintained with one of the stack classes introduced in this chapter. You may want to provide the following methods:

+   a) Method evaluatePostfixExpression, which evaluates the postfix expression.
+   b) Method calculate, which evaluates the expression op1 operator op2.

# 22.14 (Postfix Evaluator Modification) Modify the postfix evaluator program of Exercise 22.13 so that it can process integer operands larger than 9.

# 22.15 (Supermarket Simulation) Write a program that simulates a checkout line at a supermarket. The line is a queue object. Customers (i.e., customer objects) arrive in random integer intervals of from 1 to 4 minutes. Also, each customer is serviced in random integer intervals of from 1 to 4 minutes. Obviously, the rates need to be balanced. If the average arrival rate is larger than the average service rate, the queue will grow infinitely. Even with “balanced” rates, randomness can still cause long lines.

Run the supermarket simulation for a 12-hour day (720 minutes), using the following algorithm:

+   a) Choose a random integer between 1 and 4 to determine the minute at which the first customer arrives.
+   b) At the first customer’s arrival time, do the following:
+   Determine customer’s service time (random integer from 1 to 4).
+   Begin servicing the customer.
+   Schedule arrival time of next customer (random integer 1 to 4 added to the current time).
+   c) For each simulated minute of the day, consider the following:
+   If the next customer arrives, proceed as follows:
+   Say so.
+   Enqueue the customer.
+   Schedule the arrival time of the next customer.
+   If service was completed for the last customer, do the following:
+   Say so.
+   Dequeue next customer to be serviced.
+   Determine customer’s service completion time (random integer from 1 to 4 added to the current time).