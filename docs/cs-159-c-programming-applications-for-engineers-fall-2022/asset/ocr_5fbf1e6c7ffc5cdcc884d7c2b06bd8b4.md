Where are the nested loops? It is common to first consider the examples below when one thinks of nested constructs.

```
Nested while loop example:
while ( )
{
    while ( )
    {
    }
}
```

```
Nested if construct example:
if ( )
{
    if ( )
    {
    }
}
```

In the nested loop example provided on the previous page the loops are found in two different user-defined functions. One is in the main function that counts from the starting point to the ending point and the second is found in the function that calculates the factorial for each integer in the desired range.

Every loop typically represents a task, or single process, in a program. If you can identify each of these individual tasks and factor them into individual user-defined functions you may find the complex problem easier to solve and test.

# The Infinite Loop

The infinite loop is a logical error in which the condition of the loop control expression will never be false. As a logical error the form in which infinite loops may appear while the program is running can vary. One sure sign of an infinite loop is the production of infinite output. However, the error can appear in forms in which little or no output is generated.

+   You can terminate a program at any time by entering CTRL-C from the keyboard.

Example: Allow the user to enter integer values until a 1 or 2 is input.

```
int getInteger(void)
{
    int num;
    do
    {
        printf("Enter 1 or 2 -> ");
        scanf("%d", &num);
    }while(num != 1 || num != 2);
    return(num);
}
```

```
Output:
Enter 1 or 2 -> 3
Enter 1 or 2 -> 2
Enter 1 or 2 -> 1
Enter 1 or 2 ->
```

The control expression may seem logically correct, "accept input while the value entered is not 1 or 2", but logically it results in an infinite loop. There is no single value that cannot be both not 1 and not 2 at the same time.