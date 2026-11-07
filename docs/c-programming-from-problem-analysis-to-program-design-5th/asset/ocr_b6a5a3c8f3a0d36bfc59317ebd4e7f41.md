10. **(Infix to Postfix)** Write a program that converts an infix expression into an equivalent postfix expression.

The rules to convert an infix expression into an equivalent postfix expression are as follows:

Suppose `infx` represents the infix expression and `pfx` represents the postfix expression. The rules to convert `infx` into `pfx` are as follows:

+   a. Initialize `pfx` to an empty expression and also initialize the stack.
+   b. Get the next symbol, `sym`, from `infx`.
+      b.1. If `sym` is an operand, append `sym` to `pfx`.
+      b.2. If `sym` is `(`, push `sym` into the stack.
+      b.3. If `sym` is `)`, pop and append all of the symbols from the stack until the most recent left parentheses. Pop and discard the left parentheses.
+      b.4. If `sym` is an operator:
+         b.4.1. Pop and append all of the operators from the stack to `pfx` that are above the most recent left parentheses and have precedence greater than or equal to `sym`.
+         b.4.2. Push `sym` onto the stack.
+   c. After processing `infx`, some operators might be left in the stack. Pop and append to `pfx` everything from the stack.

In this program, you will consider the following (binary) arithmetic operators: +, -, *, and /. You may assume that the expressions you will process are error free.

Design a class that stores the infix and postfix strings. The class must include the following operations:

+   - **getInfix:** Stores the infix expression.
+   - **showInfix:** Outputs the infix expression.
+   - **showPostfix:** Outputs the postfix expression.

Some other operations that you might need are:

+   - **convertToPostfix:** Converts the infix expression into a postfix expression. The resulting postfix expression is stored in `pfx`.
+   - **precedence:** Determines the precedence between two operators. If the first operator is of higher or equal precedence than the second operator, it returns the value `true`; otherwise, it returns the value `false`.

Include the constructors and destructors for automatic initialization and dynamic memory deallocation.

Test your program on the following expressions: