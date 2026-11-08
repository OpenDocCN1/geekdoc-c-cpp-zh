Figure 1.5 shows the basic building blocks of a while loop. The first statement defines initialization where we have taken the COUNT variable and assigned it a value 1. Next comes the test condition, which is a decision making statement. Inside the test condition, we check whether the value of COUNT is lesser than 100 or not. If the value happens to be less, then we perform certain tasks else we exit from the flow graph. One of the actions that we perform inside the out loop is incrementing COUNT with one. Listing 1.29 illustrates the concept of looping in C:

# Listing 1.29: While Loop in C

```
```c
# include<stdio.h>

int main()
{
    int count;
    int sum=0;

    count =1;                     /* Initialization   */
    while(count <= 100)           /* Test Condition */
    {
        sum += count;
        count++;                  /* Increment Statement */

    }
    printf("\n Sum - %d ",sum);
    getch();
    return 0;
}
```
```

The lines of statement inside the curly braces that follow “while” in Listing 1.29 forms the body of the whole loop. At first, the test condition gets executed and if it is found to be true, then all the statements present inside the body of the loop get executed. The process is repeated until the test condition turns out to be false. Each execution of the loop is also known as iteration. In Listing 1.29, the statements inside the loop are going to get executed for 100 times. At the 101st iteration, the test condition fails and the control comes out of the loop. The following code snippet shows how to construct a while loop:

```
```
    Initialization of loop-control variable
    while (test condition is true)
    {
        perform certain actions;

        increment loop -control variable;

    } end loop
```
```

It should be kept in mind that a test condition should eventually turn false, else a while loop will always keep on executing endlessly.

Consider the following example:

```
```c
    int count = 10;
    while(count < 15 )
    {
        printf("\n Inside while loop");
    }
```
```

The loop given in this example will keep on executing infinitely as the test condition will never turn out to be false. A loop counter can be modified in any way possible, Any logical operation can take place on the loop counter.