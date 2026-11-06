+   - `%` remainder

*[Note: We assume left-to-right associativity for all operators for the purpose of this exercise.]* The stack should be maintained with stack nodes that contain an `int` data member and a pointer to the next stack node. You may want to provide the following functional capabilities:

+   A. function `evaluatePostfixExpression` that evaluates the postfix expression
+   B. function `calculate` that evaluates the expression `op1 operator op2`
+   C. function `push` that pushes a value onto the stack
+   D. function `pop` that pops a value off the stack
+   E. function `isEmpty` that determines if the stack is empty
+   F. function `printStack` that prints the stack

+   9. 19.14 (**Postfix Evaluation Enhanced**) Modify the postfix evaluator program of **Exercise 19.13** so that it can process integer operands larger than 9.

+   10. 19.15 (**Supermarket Simulation**) Write a program that simulates a checkout line at a supermarket. The line is a queue object. Customers (i.e., customer objects) arrive in random integer intervals of 1–4 minutes. Also, each customer is served in random integer intervals of 1–4 minutes. Obviously, the rates need to be balanced. If the average arrival rate is larger than the average service rate, the queue will grow infinitely. Even with “balanced” rates, randomness can still cause long lines.