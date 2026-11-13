
else
    push(st, (float)(exp[i]-'0'));
{
    op2 = pop(st);
    op1 = pop(st);
    switch(exp[i])
    {
        case '+':
            value = op1 + op2;
            break;
        case '-':
            value = op1 - op2;
            break;
        case '/':
            value = op1 / op2;
            break;
        case '*':
            value = op1 * op2;
            break;
        case '%':
            value = (int)op1 % (int)op2;
            break;
    }
    push(st, value);
    i++;
}
return(pop(st));
}
void push(float st[], float val)
{
    if(top==MAX-1)
        printf("\n STACK OVERFLOW");
    else
    {
        top++;
        st[top]=val;
    }
}
float pop(float st[])
{
    float val=-1;
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
Enter any postfix expression : 9 3 4 * 8 + 4 / -
Value of the postfix expression = 4.00

## Conversion of an Infix Expression into a Prefix Expression

There are two algorithms to convert an infix expression into its equivalent prefix expression. The first algorithm is given in Fig. 7.24, while the second algorithm is shown in Fig. 7.25.

- Step 1: Scan each character in the infix expression. For this, repeat Steps 2-8 until the end of infix expression
- Step 2: Push the operator into the operator stack, operand into the operand stack, and ignore all the left parentheses until a right parentheses is encountered
- Step 3: Pop operand 2 from operand stack
- Step 4: Pop operand 1 from operand stack
- Step 5: Pop operator from operator stack
- Step 6: Concatenate operator and operand 1
- Step 7: Concatenate result with operand 2
- Step 8: Push result into the operand stack
- Step 9: END

The corresponding prefix expression is obtained in the operand stack.
For example, given an infix expression (A - B / C) * (A / K - L)
Step 1: Reverse the infix string. Note that while reversing the string you must interchange left and right parentheses.
(L - K / A) * (C / B - A)

Figure 7.24 Algorithm to convert an infix expression into prefix expression

- Step 1: Reverse the infix string. Note that while reversing the string you must interchange left and right parentheses.
- Step 2: Obtain the postfix expression of the infix expression obtained in Step 1.
- Step 3: Reverse the postfix expression to get the prefix expression

Step 2: Obtain the corresponding postfix expression of the infix expression obtained as a result of Step 1.
The expression is: (L - K / A) * (C / B - A)
Therefore, [L - (K / A)] * [(C / B) - A]
= [LK/A-] * [CB/A-]
= L K A - / C B / A - *

Figure 7.25 Algorithm to convert an infix expression into prefix expression

Step 3: Reverse the postfix expression to get the prefix expression
Therefore, the prefix expression is * - A / B C - / A K L

## PROGRAMMING EXAMPLE

### 8. Write a program to convert an infix expression to a prefix expression.

```
#include <stdio.h>
#include <conio.h>
#include <string.h>
#include <ctype.h>
#define MAX 100
int stk[MAX];
int top=-1;
void reverse(char str[]);
char push(char st[], char);
char pop(char st[]);
void InfixtoPostfix(char source[], char target[]);
int getPriority(char);
char infix[100], postfix[100], temp[100];
int main()
{
clrscr();
printf("\n\n Enter any infix expression : ");
gets(infix);
strcpy(temp,infix);
reverse(temp);
InfixtoPostfix(temp, postfix);
printf("\n The corresponding postfix expression is : ");
puts(postfix);
strcpy(temp,postfix);
reverse(postfix);
}
```

```
printf("\n The prefix expression is : \n");
puts(temp);
getch();
return 0;
}
```

```
void reverse(char str[])
{
    int len, i=0, j=0;
    len=strlen(str);
    j=len-1;
    while(j>= 0)
    {
        if (str[j] == '(')
            temp[i] = ')'; 
        else if (str[j] == ')')
            temp[i] = '(';
        else
            temp[i] = str[j];
        i++;
        j--;
    }
    temp[i] = '\0';
}
```

```
void InfixtoPostfix(char source[], char target[])
{
    int i=0, j=0;
    char temp;
    strcpy(target,"");
    while(source[i]!= '\0')
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
            temp = pop(st); //remove left parentheses
            i++;
        }
        else if(isdigit(source[i]) || isalpha(source[i]))
        {
            target[j] = source[i];
            j++;
            i++;
        }
        else if ( source[i] == '+' || source[i] == '-' || source[i] == '*' ||
        source[i] == '/' || source[i] == '%')
        {
            while ( top!=-1 && (st[top]!= '(') && (getPriority(st[top])
```

```
getPriority(source[i]))) {
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
}
while(top!=-1 && (st[top]!='('))
{
    target[j] = pop(st);
    j++;
}
target[j]='\0';
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
        st[top] = val;
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
Enter any infix expression : A+B*C-D
The corresponding postfix expression is : AB+CD*- 
The prefix expression is : +*AB-CD

## Evaluation of a Prefix Expression

There are a number of techniques for evaluating a prefix expression. The simplest way of evaluation of a prefix expression is given in Fig. 7.26.

- Step 1: Accept the prefix expression
- Step 2: Repeat until all the characters in the prefix expression have been scanned
  - (a) Scan the prefix expression from right, one character at a time.
  - (b) If the scanned character is an operand, push it on the operand stack.
  - (c) If the scanned character is an operator, then the values from the operand stack
    - (i) Pop operand stack
    - (ii) Apply the operator on the popped operands
    - (iii) Push the result on the operand stack
- Step 3: END

Figure 7.26 Algorithm for evaluation of a prefix expression

| Character scanned | Operand stack |
|---|---|
| 12 | 12 |
| 4 | 12, 4 |
| / | 3 |
| 8 | 3, 8 |
| * | 24 |
| 7 | 24, 7 |
| 2 | 24, 7, 2 |
| - | 24, 5 |
| + | 29 |

For example, consider the prefix expression + - 9 2 * 7 8 / 4 12. Let us now apply the algorithm to evaluate this expression.

## PROGRAMMING EXAMPLE

### 9. Write a program to evaluate a prefix expression.

```
#include <stdio.h>
#include <conio.h>
#include <ctype.h>
#include <string.h>
int stk[10];
int top=-1;
int pop();
void push(int);
void main()
{
   char prefix[10];
   int len, val, i, opr1, opr2, res;
   clrscr();
   printf("\n Enter the prefix expression : ");
   gets(prefix);
   len = strlen(prefix);
   for(i=len-1;i>=0;i--)
   {
      switch(get_type(prefix[i]))
      {
         case 0:
         val = prefix[i] - '0';
         push(val);
         break;
         case 1:
         opr1 = pop();
         opr2 = pop();
         switch(prefix[i])
         {
            case '+':
            res = opr1 + opr2;
            break;
            case '-':
            res = opr1 - opr2;
            break;
            case '*':
            res = opr1 * opr2;
            break;
            case '/':
            res = opr1 / opr2;
            break;
         }
         push(res);
      }
   }
   printf("\n RESULT = %d", stk[0]);
   getche();
   return 0;
}
void push(int val)
{
   stk[++top] = val;
}
```

```
}
int pop()
{
return(stk[top--]);
}
int get_type(char c)
{
if(c == '*' || c == '-' || c == '+' || c == '/')
return 1;
else return 0;
}
```

**Output**
Enter the prefix expression : +-927
RESULT = 14

## 7.7.4 Recursion

In this section we are going to discuss recursion which is an implicit application of the STACK ADT.

A recursive function is defined as a function that calls itself to solve a smaller version of its task until a final call is made which does not require a call to itself. Since a recursive function repeatedly calls itself, it makes use of the system stack to temporarily store the return address and local variables of the calling function. Every recursive solution has two major cases. They are

- Base case, in which the problem is simple enough to be solved directly without making any further calls to the same function.
- Recursive case, in which first the problem at hand is divided into simpler sub-parts. Second the function calls itself but with sub-problems of the problem obtained in the first step. Third, the result is obtained by combining the solutions of simpler sub-parts.

Therefore, recursion is defining large and complex problems in terms of smaller and more easily solvable problems. In recursive functions, a complex problem is defined in terms of simpler problems and the simplest problem is given explicitly.

To understand recursive functions, let us take an example of calculating factorial of a number. To calculate n!, we multiply the number with factorial of the number that is 1 less than that number. In other words, n! = n X (n-1)!

Let us say we need to find the value of 5!

5! = 5 X 4 X 3 X 2 X 1
= 120

This can be written as

5! = 5 X 4!, where 4! = 4 X 3!

Therefore,

5! = 5 X 4 X 3!

Similarly, we can also write,

| PROBLEM | SOLUTION |
| :--- | :--- |
| 5! | 5 x 4 x 3 x 2 x 1! |
| = 5 x 4! | = 5 x 4 x 3 x 2 x 1 |
| = 5 x 4 x 3! | = 5 x 4 x 3 x 2 |
| = 5 x 4 x 3 x 2! | = 5 x 4 x 6 |
| = 5 x 4 x 3 x 2 x 1! | = 5 x 24 |
| = 5 x 4 x 3 x 2 x 1 | = 120 |
| = 120 | |

Figure 7.27 Recursive factorial function

5! = 5 x 4 x 3 x 2 x 1!
Expanding further
5! = 5 x 4 x 3 x 2 x 1!
We know, 1! = 1
The series of problems and solutions can be given as shown in Fig. 7.27.

Now if you look at the problem carefully, you can see that we can write a recursive function to calculate the
