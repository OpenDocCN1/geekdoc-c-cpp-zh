+   Step 1: Add a ")" at the end of the postfix expression
+   Step 2: Scan every character of the postfix expression and repeat Steps 3 and 4 until ")" is encountered
+   Step 3: If an operand is encountered, push it on the stack. If an operator * is encountered, then
+       a. Pop the top two elements from the stack as A and B and
+       b. Evaluate B O A, where A is the topmost element and B is the element below A.
+       c. Push the result of evaluation on the stack
+       [END OF IF]
+   Step 4: SET RESULT equal to the topmost element of the stack
+   Step 5: EXIT

| Character Scanned | Stack |
|---|---|
| 9 | 9 |
| 3 | 9, 3 |
| 4 | 9, 3, 4 |
| * | 9, 12 |
| 8 | 9, 12, 8 |
| + | 9, 20 |
| 4 | 9, 20, 4 |
| / | 9, 5 |
| - | 4 |

# Figure 7.23 Algorithm to evaluate a postfix expression

Let us now take an example that makes use of this algorithm. Consider the infix expression given as 9 – ((3 * 4) + 8) / 4. Evaluate the expression.

The infix expression 9 – ((3 * 4) + 8) / 4 can be written as 9 3 4 * 8 + 4 / – using postfix notation. Look at Table 7.1, which shows the procedure.

# Programming Example

+   7. Write a program to evaluate a postfix expression.

```
#include <stdio.h>
#include <conio.h>
#include <ctype.h>
#define MAX 20
float st[MAX];
int top=-1;
void push(float st[], float val);
float pop(float st[]);
float evaluatePostfixExp(char exp[]);
int main()
{
    float val;
    char exp[100];
    clrscr();
    printf("\n Enter any postfix expression : ");
    gets(exp);
    val = evaluatePostfixExp(exp);
    printf("\n Value of the postfix expression = %.2f", val);
    getch();
    return 0;
}
float evaluatePostfixExp(char exp[])
{
    int i=0;
    float op1, op2, value;
    while(exp[i] != '\0')
    {
        if(isdigit(exp[i]))
```