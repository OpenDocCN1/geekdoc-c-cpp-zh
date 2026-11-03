```
```c
}

return(0);
}
```
```

The code above is basically a rewrite of the codes we used before, but we added in the else statement. In line ten, we used the if condition in order to make the evaluation. This statement is going to be executed if that condition is evaluated as true. If the condition is evaluated and seen as false, the statement that is with the else part of the code will be executed. Take a moment to build and run this code and try out a few inputs to see how it works.

Note in this code that I didn’t use a semi-colon, but instead of a curly bracket. You could write it all out without using the brackets since there is only one statement, but this is a great way to write it out to make sure that it all stays together and it is good programming practice.

# ### Else If Statements

There are times when you will have at least three, if not more, conditions that you want to use inside of your code. In these instances, you would need something a bit different than the if and the else statements. This is when we will use at the structure for the else if statements. Let’s take a look at the following code to see how the else if statements would work.

```
```c
#include <stdio.h>

int main()
{
    Int a;

    Printf(“Type an integer: “);
    Scanf(“%d”, &a);
    Printf(“You typed %d. \n” ,a);
```
```