for the time the loop is running. For example, let us try to print a message Loops Made Simple 5 times using for loop. The sample code is as given below:

```
```c
#include<stdio.h>
void main()
{
    for(int i=1; i<=5; i++)
    {
    printf("Loops Made Simple\n");
    i++;
    }
    /*Value of variable i cannot be accessed outside the loop*/
}
```
```

Note that variable i is within the loop and its job is only to count the number of iterations of the loop. The loop has five iterations because it is executed from i=1 to 5. The value of variable i reaches 6, the loop terminates and hence the variable i is destroyed. This is because the variable was declared within the loop and it cannot be accessed outside the loop in any manner.

If you want to access the value of variable i even outside the loop, you should not create it as a local variable of the loop. This means that you have to declare variable i, outside the loop as shown in the following program:

```
```c
#include<stdio.h>
void main()
{
    int i; /*variable i is declared outside the loop */
    for(i=1; i<=5; i++)
    {
        printf("Loops Made Simple\n");
        i++;
    }
    /*Value of variable i can be accessed outside the loop*/
    printf("Value of variable i outside the loop is %d",i);
}
```
```

Given that variable i is declared outside the loop, we are able to print its value even after the execution of the loop is completed. The last printf statement prints the value of i as 6, as 6 is the first value of i when the loop terminates.

Value of variable i outside the loop is 6

# ### 5.9 Empty Loops

A loop that has no operation to perform is called an empty loop. For example, see the following loop: