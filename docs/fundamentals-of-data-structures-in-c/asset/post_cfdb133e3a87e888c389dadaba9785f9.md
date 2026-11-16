
- Consider the part of the expression converted to postfix as a single operand = Z-E [Z=(+YX)]
- Parenthesize the sub-expression with the operator having the highest priority from left to right = (Z-E)
- Move the operand inside parenthesis to the left of the operand = (-ZE)
- Substitute the value for z = (-(+YX) E)
- Substitute the value for Y = (- (+(*AB) X) E)
- Substitute the value for X = (- (+(*AB) (/CD) ) E)
- Remove all parenthesis = -*+AB/CDE
- The required prefix form is -*+AB/CDE.

## 3.8.2 Converting Infix Expression to Postfix Form

Evaluation of an expression using computers can be done in different ways. Some programmers may try to parse the expression and find out the operators that have the highest priority, calculate them and later evaluate the expression with operators of lower priority. But if parenthesis and functions are added to the expression it will soon be very complicated to do the calculation. An easier way to calculate it is to convert the expression from infix notation to postfix notation. This may first look very strange but this is much easier when we need to do calculations on a computer.

### The following procedure is used to convert infix to postfix expression

- Read the infix string.
- Traverse from left to right of the expression.
- If an operand is encountered, add to the postfix string.
- If an operator is encountered push it on the stack, if any of the following conditions are satisfied.
  - The stack is empty.
  - If the precedence of the operator at the top of the stack is of lower priority than the operator being processed.
- If all the above condition fails, then pop the operator being processed to the postfix string.
- When the infix string is empty, pop the elements of the stack onto the postfix string to get the result.

### Algorithm for Infix to Postfix Conversion

IN_TO_POST(INSTR : STRING, POSTSTR : STRING)

Where INSTR contains infix expression & POSTSTR stores the resultant expression

Step 1 : Initialize the Stack

Step 2 : While (INSTR != NULL)

Step 3 : CH = get the character from INSTR

Step 4 : If (CH == operand) Then
         Append CH into POSTSTR
         Else If (CH == '(') Then
         Push CH into the Stack
         Else If (CH == ')') Then
         Pop the data from the Stack and append the data into POSTSTR until
         we get '(' from the Stack
         Else
         While (precedence(Top of the Stack) >= precedence(CH))
         Pop the data from the Stack and append the data into POSTSTR
         [End of While Structure]
         [End of Step 4 If Structure]

Step 5 : Push CH into the Stack.

Step 6 : [End of Step 2 While Structure]

Step 7 : Pop all the data from the Stack and append the data into POSTSTR until
         Stack is Empty

END_IN_TO_POST()

### Program 3.5

```c
/* Program to convert infix expression to postfix notation. */
/* in_post.c */
/* */
#include <stdio.h>
#include <ctype.h>
#include <string.h>
#define MAX 9
typedef struct node
{
 char data;
 struct node *next;
}stack;
int push(char);
int pop(char *);
stack *getNode();
void releaseNode(stack *);
void inToPost(char [], char []);
int indexPriority(char P[][2], char data);
stack *topStk = NULL;
```

```c
char ip[MAX][2] = {
    {'(', MAX}, {')', 0 }, {'\0', 0}, {'+', 1},
    {'-', 1}, {'*', 2}, {'/', 2}, {'%', 2},
    {'\0', 3}
};
```

```c
char sp[MAX][2] = {
    {'(', 0}, {')', -1}, {'\0', 0}, {'+', 1},
    {'-', 1}, {'*', 2}, {'/', 2}, {'%', 2},
    {'\0', 3}
};
```

```c
void main()
{
    char inStr[20], postStr[20];
    printf("Enter the infix expression : ");
    scanf("%s", inStr);
    inToPost(inStr, postStr);
    printf("The postfix expression is : %s", postStr);
}
```

```c
int push(char value)
{
    extern stack *topStk;
    stack *newptr;
    newptr = getNode();
    if(newptr == NULL)
    return -1;
    newptr -> data = value;
    newptr -> next = topStk;
    topStk = newptr;
    return 0;
}
```

```c
int pop(char *value)
{
    extern stack *topStk;
    stack *temp;
    if(topStk == NULL)
    return -1;
    temp = topStk;
    topStk = topStk -> next;
    *value = temp -> data;
    releaseNode(temp);
    return 0;
}
```

```c
stack *getNode()
{
    return ((stack *)malloc(sizeof(stack)));
}

void releaseNode(stack *newnode)
{
    free(newnode);
}

void inToPost(char inStr[], char postStr[])
{
    char ch, item;
    int i = 0, st = 0, spr, ipr;
    push('\0');
    while((ch = inStr[st++]) != NULL)
    {
        if(tolower(ch) >= 'a' && tolower(ch) <= 'z')
            postStr[i++] = ch;
        else if(ch == '(')
            push(ch);
        else if(ch == ')')
        {
            pop(&item);
            while(item != '(')
            {
                postStr[i++] = item;
                pop(&item);
            }
        }
        else
        {
            pop(&item);
            spr = indexPriority(sp, item);
            ipr = indexPriority(ip, ch);
            while(sp[spr][1] >= ip[ipr][1])
            {
                postStr[i++] = item;
                pop(&item);
                spr = indexPriority(sp, item);
            }
        }
        push(item);
        push(ch);
    }
    while(!pop(&item))
    postStr[i++] = item;
}
```

```c
int indexPriority(char P[][2], char data)
{
    int ind;
    for(ind = 0; ind < MAX; ind++)
    if(P[ind][0] == data)
    return ind;
}
```

The program displays the following output

RUN1 Enter the infix expression : a-b*c+d/g
The postfix expression is : abc-*dg/+

RUN2 Enter the infix expression : (A+B)*(C-D)%G
The postfix expression is : AB+CD--G/

## 3.8.3 Evaluating an Expression in Postfix Notation

Evaluating an expression in postfix notation is trivially easy if you use a stack. The postfix expression to be evaluated is scanned from left to right. Variables or constants are pushed onto the stack. When an operator is encountered, the indicated action is performed using the top two elements of the stack, and the result replaces the operands on the stack.

### Steps to be noted while evaluating a postfix expression using a stack

- Traverse from left to right of the expression.
- If an operand is encountered, push it onto the stack.
- If you see a binary operator, pop two elements from the stack, evaluate those operands with that operator, and push the result back in the stack.
- If you see a unary operator, pop one element from the stack, evaluate those operands with that operator, and push the result back in the stack.
- When the evaluation of the entire expression is over, the only thing left on the stack should be the final result. If there are zero or more than 1 operands left on the stack, either your program is inconsistent, or the expression was invalid.

### Algorithm to Evaluate a Postfix Expression

- EVALPOST(POSTEXP : STRING)
- Where POSTEXP contains postfix expression
- Step 1 : Initialize the Stack.
- Step 2 : While (POSTEXP != NULL)
- Step 3 : ch = get the character from POSTEXP
- Step 4 : If (ch == Operand) Then
  - Read the value for CH and Push CH into Stack
  - Else If (ch == Operator) Then
    - Pop the two operands from the Stack and perform arithmetic operation
      with the operator and Push the resultant value into the Stack
    - [End of Step 4 if Structure]
- Step 5 : [End of Step 2 While Structure]
- Step 6 : Pop the data from the Stack and return the popped data
- END EVALPOST()

### Program 3.6

```c
/* Program to evaluate postfix expression using stacks. */
/* evalpost.c */
#include<stdio.h>
#include<ctype.h>
#include<stdlib.h>
typedef struct node
{
    int data;
    struct node *next;
}stack;
stack *topStk = NULL;
int push(int);
int pop(int );
stack *getNode();
int evalPost(char []);
int calc(int, int, char);
void printError();
void main()
{
    char postStr[20];
    printf("\nEnter the postfix string : ");
    gets(postStr);
    printf("\nThe evaluated value of %s is %d",postStr, evalPost( postStr) );
}
```
