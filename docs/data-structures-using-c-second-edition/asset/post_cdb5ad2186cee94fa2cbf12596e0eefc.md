
The algorithm given below transforms an infix expression into postfix expression, as shown in Fig. 7.22. The algorithm accepts an infix expression that may contain operators, operands, and parentheses. For simplicity, we assume that the infix operation contains only modulus (%), multiplication (*), division (/), addition (+), and subtraction (-) operators and that operators with same precedence are performed from left-to-right.

The algorithm uses a stack to temporarily hold operators. The postfix expression is obtained from left-to-right using the operands from the infix expression and the operators which are removed from the stack. The first step in this algorithm is to push a left parenthesis on the stack and to add a corresponding right parenthesis at the end of the infix expression. The algorithm is repeated until the stack is empty.

- Step 1: Add ")" to the end of the infix expression
- Step 2: Push "(" on to the stack
- Step 3: Repeat until each character in the infix notation is scanned
  - If a "(" is encountered, push it on the stack
  - If an operand (whether a digit or a character) is encountered, add it to the postfix expression
  - If a ")" is encountered, then
    - a. Repeatedly pop from stack and add it to the postfix expression until a "(" is encountered.
    - b. Discard the ")". That is, remove the "(" from stack and do not add it to the postfix expression
  - If an operator O is encountered, then
    - a. Repeatedly pop from stack and add each operator (popped from the stack) to the postfix expression which has the same precedence or a higher precedence than O
    - b. Push operator O on to the stack.
    - [END OF IF]
- Step 4: Repeatedly pop from the stack and add it to the postfix expression until the stack is empty
- Step 5: EXIT

Figure 7.22 Algorithm to convert an infix notation to postfix notation

## Solution

| Infix Character Scanned | Stack | Postfix Expression |
|---|---|---|
| A | ( | A |
| - | ( - | A |
| ( | ( - ( | A |
| B | ( - ( / | A B |
| / | ( - ( / | A B |
| C | ( - ( / | A B C |
| ) | ( - ( | A B C / |
| + | ( - + | A B C / |
| * | ( - + * | A B C / |
| D | ( - + * ( | A B C / D |
| % | ( - + * ( % | A B C / D |
| E | ( - + * ( % | A B C / D E |
| * | ( - + * ( % * | A B C / D E |
| F | ( - + * ( % * | A B C / D E F |
| ) | ( - + * | A B C / D E F * % |
| / | ( - + * / | A B C / D E F * % / |
| G | ( - + * / | A B C / D E F * % / G |
| ) | ( - + | A B C / D E F * % / G + |
| * | ( - * | A B C / D E F * % / G + * |
| H | ( - * | A B C / D E F * % / G + * H |
| ) | ( | A B C / D E F * % / G + * H - |

### Example 7.3 Convert the following infix expression into postfix expression using the algorithm given in Fig. 7.22.
(a) A – ( B / C + ( D % E * F ) / G) * H
(b) A – (B / C + (D % E * F) / G) * H

### PROGRAMMING EXAMPLE
6. Write a program to convert an infix expression into its equivalent postfix notation.

```c
#include <stdio.h>
#include <conio.h>
#include <ctype.h>
#include <string.h>
#define MAX 100
char st[MAX];
int top=-1;
void push(char st[], char);
char pop(char st[]);
void InfixtoPostfix(char source[], char target[]);
int getPriority(char);
int main()
{
    char infix[100], postfix[100];
    clrscr();
    printf("\n Enter any infix expression : ");
    gets(infix);
    strcpy(postfix, "");
    InfixtoPostfix(infix, postfix);
    printf("\n The corresponding postfix expression is : ");
    puts(postfix);
    getch();
    return 0;
}
void InfixtoPostfix(char source[], char target[])
{
    int i=0, j=0;
    char temp;
    strcpy(target,"");
    while(source[i]!='\0')
    {
        if(source[i]=='(')
        {
            push(st, source[i]);
            i++;
        }
        else if(source[i] == ')')
        {
            while((top!=-1) && (st[top]!='('))
            {
                target[j] = pop(st);
                j++;
            }
            if(top==-1)
            {
                printf("\n INCORRECT EXPRESSION");
                exit(1);
            }
            temp = pop(st); //remove left parenthesis
            i++;
        }
        else if(isdigit(source[i]) || isalpha(source[i]))
        {
            target[j] = source[i];
            j++;
            i++;
        }
        else if (source[i] == '*' || source[i] == '-' || source[i] == '+' ||
                 source[i] == '/' || source[i] == '%')
        {
            while (top!=-1 && (st[top]!= '(') && (getPriority(st[top]) > getPriority(source[i])))
            {
                target[j] = pop(st);
                j++;
            }
            push(st, source[i]);
            i++;
        }
        else
        {
            printf("\n INCORRECT ELEMENT IN EXPRESSION");
            exit(1);
        }
        while((top!=-1) && (st[top]!='('))
        {
            target[j] = pop(st);
            j++;
        }
        target[j]='\0';
    }
}
int getPriority(char op)
{
    if(op=='/' || op == '*' || op=='%')
        return 1;
    else if(op=='+' || op=='-')
        return 0;
}
void push(char st[], char val)
{
    if(top==MAX-1)
        printf("\n STACK OVERFLOW");
    else
    {
        top++;
        st[top]=val;
    }
}
char pop(char st[])
{
    char val=' ';
    if(top==-1)
        printf("\n STACK UNDERFLOW");
    else
    {
        val=st[top];
        top--;
    }
    return val;
}
```

**Output**
Enter any infix expression : A+B*C+D
The corresponding postfix expression is : AB+CD*=

## Evaluation of a Postfix Expression

The ease of evaluation acts as the driving force for computers to translate an infix notation into a postfix notation. That is, given an algebraic expression written in infix notation, the computer first converts the expression into the equivalent postfix notation and then evaluates the postfix expression.

Both these tasks—converting the infix notation into postfix notation and evaluating the postfix expression—make extensive use of stacks as the primary tool.

Using stacks, any postfix expression can be evaluated very easily. Every character of the postfix expression is scanned from left to right. If the character encountered is an operand, it is pushed on to the stack. However, if an operator is encountered, then the top two values are popped from the stack and the operator is applied on these values. The result is then pushed on to the stack.

Let us look at Fig. 7.23 which shows the algorithm to evaluate a postfix expression.

- Step 1: Add a ")" at the end of the postfix expression
- Step 2: Scan every character of the postfix expression and repeat Steps 3 and 4 until ")" is encountered
- Step 3: If an operand is encountered, push it on the stack. If an operator * is encountered, then
  - a. Pop the top two elements from the stack as A and B and
  - b. Evaluate B O A, where A is the topmost element and B is the element below A.
  - c. Push the result of evaluation on the stack
  - [END OF IF]
- Step 4: SET RESULT equal to the topmost element of the stack
- Step 5: EXIT

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

### Figure 7.23 Algorithm to evaluate a postfix expression

Let us now take an example that makes use of this algorithm. Consider the infix expression given as 9 – ((3 * 4) + 8) / 4. Evaluate the expression.

The infix expression 9 – ((3 * 4) + 8) / 4 can be written as 9 3 4 * 8 + 4 / – using postfix notation. Look at Table 7.1, which shows the procedure.

## Programming Example

- 7. Write a program to evaluate a postfix expression.

```c
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
