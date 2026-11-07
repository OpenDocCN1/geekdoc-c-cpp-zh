+   1. Push a left parenthesis `(` onto the stack.
+   2. Append a right parenthesis `)` to the end of `infix`.
+   3. While the stack is not empty, read `infix` from left to right and do the following:
+      - If `infix`’s current character is a digit, copy it to the next element of `postfix`.
+      - If `infix`’s current character is a left parenthesis, push it onto the stack.
+      - If `infix`’s current character is an operator:
+        - Pop operators (if there are any) off the top of the stack while they have equal or higher precedence than the current operator, and insert the popped operators in `postfix`.
+        - Push the current character in `infix` onto the stack.
+      - If `infix`’s current character is a right parenthesis:
+        - Pop operators from the top of the stack and insert them in `postfix` until a left parenthesis is at the top of the stack.
+        - Pop (and discard) the left parenthesis from the stack.

The following arithmetic operations are allowed in an expression:

+   - `+` addition
+   - `-` subtraction
+   - `*` multiplication
+   - `/` division

The stack should be maintained with the following declarations:

```
struct stackNode {
    char data;
    struct stackNode *nextPtr;
};

typedef struct stackNode StackNode;
typedef StackNode *StackNodePtr;
```

The program should consist of main and eight other functions with the following function prototypes:

| Function prototype | Description |
|---|---|
| `void convertToPostfix(char infix[], char postfix[]);` | Convert the infix expression to postfix notation. |
| `bool isOperator(char c);` | Return true if `c` is an operator; otherwise, return false. Recall that `bool`, `true` and `false` are defined in `stdbool.h`. |
| `int precedence(char operator1, char operator2);` | Return -1, 0 or 1 to indicate whether the precedence of `operator1` is less than, equal to, or greater than the precedence of `operator2`, respectively. |
| `void push(StackNodePtr *topPtr, char value);` | Push a value onto the stack. |