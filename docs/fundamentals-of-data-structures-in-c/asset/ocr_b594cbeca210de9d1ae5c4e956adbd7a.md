# Algorithm to Evaluate a Postfix Expression

+   EVALPOST(POSTEXP : STRING)
+   Where POSTEXP contains postfix expression
+   Step 1 : Initialize the Stack.
+   Step 2 : While (POSTEXP != NULL)
+   Step 3 : ch = get the character from POSTEXP
+   Step 4 : If (ch == Operand) Then
+   Read the value for CH and Push CH into Stack
+   Else If (ch == Operator) Then
+   Pop the two operands from the Stack and perform arithmetic operation
+   with the operator and Push the resultant value into the Stack
+   [End of Step 4 if Structure]
+   Step 5 : [End of Step 2 While Structure]
+   Step 6 : Pop the data from the Stack and return the popped data
+   END EVALPOST()

# Program 3.6 :

```
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