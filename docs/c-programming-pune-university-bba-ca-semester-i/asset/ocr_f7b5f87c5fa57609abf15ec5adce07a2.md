The control flow can be increment or decrement value of variable depending on requirements.

Expression1 is used to initialize the loop; expression2 is used to determine whether or not the loop will continue; expression3 is evaluated at the end of each iteration or cycle.

**NOTE 1:** Expression2 is tested before the stmt and expression3 is executed; it is possible that the body of the loop is never executed or tested.

**NOTE 2:** Any or all of the 3 expressions in a for loop can be omitted, but the 2 semi-colons must remain. Like **for( ; ; )**

If expression1 is omitted, there is no initialization done in the loop, but you might not need any initialization for your program.

Like :

```
```c
i=1;
for ( ; i<=10;i++)
```
```

If expression2 is omitted, there is no test section so you will essentially have an infinite loop.

```
```c
for(i=1; ; i++)
```
```

If expression3 is omitted, there is no update as part of the for statement, but the update could be done as part of the statement in the body of the loop.

```
```c
for(i=1;i<=10; )
{
    printf("%d",i);
    i++;
}
```
```

The **for** loop is commonly used when the number of iterations is known.

In general, a for loop can be written as an equivalent to a while loop and *vice versa*.

```
```c
for (expression1; expression2; expression3)
    statement;
```
```

**is equivalent to...**

```
```c
expression1;
while (expression2)
{
    Statements;
    expression3;
}
```
```