# **NOTES**

break statement is also used to break the switch block as discussed in Chapter 4. Hence break statement, in C/C++ can be used to break the **switch block** or it can be used to break the **loop**. However, continue statement is designed to operate only with loops and it will make no sense to use it with any of the decision making control structures like switch block for example.

> > Will the break statement terminate if it is written within the switch block which is inside the loop?

If the switch block is present inside the loop and if the break statement is written within the switch block, it will only exit the switch block and not the loop. For example, consider pseudo code below:

```
    while(Looping condition )
    {
        switch(expression)
        {
            case Value 1: operation 1;
                break;
            case Value 2:operation 2;
                break;
            ......;
            default: default operation;
        }
    }
```

If you intend to terminate the loop, in this case, you must write the break statement outside the switch block. Similarly, if there is a nesting of loops in your program, the break statement will only terminate the innermost loop in which it is written. Do not expect the break statement to terminate all the loops together. As shown below, there are three while loops one inside another and the break statement is written in the innermost loop. In this case, the break statement will only terminate the inner most loop and the execution of outer loops will continue as usual

```
    while (Looping condition 1)
    {
        while (condition 2)
        {
            while(condition 3)
            {
                .........
                .........
                break;
                .........
                .........
            }
        }
    }
```

# **5.5.1 To check if the number is prime or not: An example**

Let us write a program to take a number as input from the user and to check if the number is prime or not.