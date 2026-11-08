+   b.4. If sym is an operator:
+   
+   b.4.1. Pop and append all of the operators from the stack to pfx that are above the most recent left parentheses and have precedence greater than or equal to sym.
+   
+   b.4.2. Push sym onto the stack.
+   
+   c. After processing infix, some operators might be left in the stack. Pop and append to pfx everything from the stack.

In this program, you will consider the following (binary) arithmetic operators: +, −, *, and /. You may assume that the expressions you will process are error free.

Design a class that stores the infix and postfix strings. The class must include the following operations:

+   - **getInfix**: Stores the infix expression.
+   - **showInfix**: Outputs the infix expression.
+   - **showPostfix**: Outputs the postfix expression.

Some other operations that you might need are:

+   - **convertToPostfix**: Converts the infix expression into a postfix expression. The resulting postfix expression is stored in pfx.
+   - **precedence**: Determines the precedence between two operators. If the first operator is of higher or equal precedence than the second operator, it returns the value true; otherwise, it returns the value false.

Include the constructors and destructors for automatic initialization and dynamic memory deallocation.

Test your program on the following expressions:

+   a.  A + B − C;
+   
+   b.  (A + B) * C;
+   
+   c.  (A + B) * (C − D);
+   
+   d.  A + ((B + C) * (E − F) − G) / (H − I);
+   
+   e.  A + B * (C + D) − E / F * G + H;

For each expression, your answer must be in the following form:

```
Infix Expression: A + B − C;
Postfix Expression: A B + C −
```

11. Write the definitions of the functions to overload the assignment operator and copy constructor for the class queueType. Also, write a program to test these operations.

12. Write the definitions of the functions to overload the assignment operator and copy constructor for the class linkedQueueType. Also, write a program to test these operations.