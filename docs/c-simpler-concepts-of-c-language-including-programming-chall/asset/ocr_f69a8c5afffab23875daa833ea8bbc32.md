# OPERATORS 69

# Increment Operator (++)

This operator is useful in many places as it allows the programmer's job and saves time (literally reducing the time to type!). The ultimate aim of this operator is to increment the value of operand by 1. There are two kinds of increment operators based on the operations performed.

+   1. Pre increment - First value of the operand is incremented; assigned to the left hand side of the expression.
2. Post increment -First current value of the operand is assigned to the left hand side of the expression, and the operand is incremented by one!

# Example

int a=10,b;
a++; $ightarrow$ assigns 10 to b first; then increases the value of a by 1.
printf("%d",b); $ightarrow$ 10 is printed!
b+=a; $ightarrow$ increases the value of a by 1; then assigns the incremented value is assigned to b;
printf("%d",b); $ightarrow$ 12 is printed. (Since, after b=a, a's value would have become 11; then after b+=a, it becomes 12.)
Now, the reader would got a clear picture about increment operators. Next, decrement operators are discussed.

# Decrement Operator (-)

This operator performs in the way just opposite to the increment operator. It decreases the value of the operand by 1. Similar to increment operator, it has two versions,

+   1. Pre decrement - First value of the operand is decremented by one; then assigned to the left hand side of the expression.
2. Post decrement - First current value of the operand is assigned to the left hand side of the expression, and the operand is decremented by one!

# Examples

int a=10,b;
a--; $ightarrow$ assigns 10 to b first; then decreases the value of a by 1.
printf("%d",b); $ightarrow$ 9 is printed!
b-=a; $ightarrow$ decreases the value of a by 1; then assigns the decremented value is assigned to b;
printf("%d",b); $ightarrow$ 8 is printed.
Refer to Program 4.7 for reference.

```
#include<stdio.h>
void main() {
    int a;
    printf("Unary operators example..\n\n");
    printf("enter the value if 'a':");scanf("%d",&a);
    printf("Pre Increment operator : ++a=%d\n",++a);
    printf("Pre Decrement operator : --a=%d\n",--a);
    printf("Post Increment operator : a++=%d\n",a++);
    printf("Post Decrement operator : a--=%d--\n",a--);
    printf("After decrementing, a=%d\n",a);
    getch();
}
```

# Program 4.7 Unary operators example