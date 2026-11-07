The arithmetic operations allowed in an expression are:

+   - `+` addition
+   - `-` subtraction
+   - `*` multiplication
+   - `/` division

The stack should be maintained with the following declarations:

```
```c
struct stackNode {
    int data;
    struct stackNode *nextPtr;
};
typedef struct stackNode StackNode;
typedef StackNode *StackNodePtr;
```
```

The program should consist of main and six other functions with the following function prototypes:

| Function prototype | Description |
|---|---|
| `int evaluatePostfixExpression(char *expr);` | Evaluate the postfix expression and return its result. |
| `int calculate(int op1, int op2, char operator);` | Evaluate the expression op1 operator op2 and return its result. |
| `void push(StackNodePtr *topPtr, int value);` | Push a value onto the stack. |
| `int pop(StackNodePtr *topPtr);` | Pop a value off the stack and return that value. |
| `bool isEmpty(StackNodePtr topPtr);` | Return true if the stack is empty (that is, topPtr is NULL); otherwise, return false. |
| `void printStack(StackNodePtr topPtr);` | Print the stack—this function traverses the linked list that implements the stack, but does not modify it. |

12.24 (The Simple Programming Language—Writing Simple Programs) Before building the compiler, let's discuss a simple yet powerful, high-level language similar to early versions of the BASIC programming language. We call the language Simple. Every Simple statement consists of a line number and a Simple instruction. Line numbers must appear in ascending order. Each instruction begins with one of the following Simple commands: rem, input, let, print, goto, if...goto or end, which we describe in the following table. Simple evaluates only integer expressions using the +, -, * and / operators. These operators have the same precedence as in C. Parentheses can change an expression's order of evaluation. Exercise 12.27 suggests enhance-