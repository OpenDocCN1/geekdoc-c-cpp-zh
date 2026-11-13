```
#include <conio.h>
int stk[10];
int top=-1;
int pop();
void push(int);
int main()
{
    int val, n, i,
    arr[10];
    clrscr();
    printf("\n Enter the number of elements in the array : ");
    scanf("%d", &n);
    printf("\n Enter the elements of the array : ");
    for(i=0;i<n;i++)
    {
    scanf("%d", &arr[i]);
    }
    for(i=0;i<n;i++)
    push(arr[i]);
    for(i=0;i<n;i++)
    {
    val = pop();
    arr[i] = val;
    }
    printf("\n The reversed array is : ");
    for(i=0;i<n;i++)
    printf("%d ", arr[i]);
    getche();
    return 0;
}
void push(int val)
{
    stk[++top] = val;
}
int pop()
{
    return(stk[top--]);
}
Output
Enter the number of elements in the array : 5
Enter the elements of the array : 1 2 3 4 5
The reversed array is : 5 4 3 2 1
```

# 7.7.2 Implementing Parentheses Checker

Stacks can be used to check the validity of parentheses in any algebraic expression. For example, an algebraic expression is valid if every open bracket there is a corresponding closing bracket. For example, the expression (A+B) is invalid but an expression {A + (B – C)} is valid. Look at the program below which traverses an algebraic expression to check for its validity.

# PROGRAMMING EXAMPLE

+   5. Write a program to check nesting of parentheses using a stack.

```
#include <stdio.h>
#include <conio.h>
#include <string.h>
#define MAX 10
char stk[MAX];
int top=-1;
void push(char);
```