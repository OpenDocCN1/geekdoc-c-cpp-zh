(condition)? expression1: expression2

The above syntax states that if the condition in the brackets is evaluated to be true then expression 1 is to be returned but if it turns out to be false then expression 2 has to be returned. In short the question mark(?) resembles the if statement and the colon(:) the else statement.

Things will be unambiguous when the following example is comprehended.

```
```c
#include<stdio.h>
main()
{
    int a, b;
    printf(“enter a value for a:”);
    scanf(“%d”, &a); b=(a>6? 2: 3);
    printf(“the value of b is:%d”, b);
}
```
```

In the above example one can observe that the condition to be validated is whether the entered number for a is greater than 6 or not. If the number is greater then the number 2 must be stored in b, if it not greater then the number 3 is to be stored.

# 3.12. DO’S AND DON’TS

+   - **Do’s:** The *if* statement is executed only if the condition following it becomes true. The condition should be enclosed within a pair of parenthesis. The statements following the condition should be terminated using a semicolon. In the for statements the initialization, condition, and the incrementation is done within a pair of parenthesis. Between each of the expressions in the for loop there must be a semicolon. The label in a goto should be followed by a colon.
+   - **Don’ts:** The choice within the parenthesis of the switch case cannot take a floating point. The goto should be avoid as far as possible.