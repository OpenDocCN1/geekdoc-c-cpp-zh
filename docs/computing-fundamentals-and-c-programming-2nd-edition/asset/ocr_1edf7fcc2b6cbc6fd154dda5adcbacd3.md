continues until the test-condition finally becomes *false* and the control is transferred out of the loop. On exit, the program continues with the statement immediately after the body of the loop.

The body of the loop may have one or more statements. The braces are needed only if the body contains two or more statements. However, it is a good practice to use braces even if the body has only one statement.

We can rewrite the program loop discussed in Section 8.1 as follows:

```
    ========
    sum = 0;
    n = 1;                    /* Initialization */
    while(n <= 10)            /* Testing */
    {
        sum = sum + n * n;    /* Incrementing */
        n = n+1;
    }
    printf("sum = %d\n", sum);
    ========
```

The body of the loop is executed 10 times for n = 1, 2, ....., 10, each time adding the square of the value of n, which is incremented inside the loop. The test condition may also be written as **n < 11**; the result would be the same. This is a typical example of counter-controlled loops. The variable n is called *counter* or *control variable*.

Another example of **while** statement, which uses the keyboard input is shown below:

```
    ========
    character = ' ';
    while (character != 'Y')
        character = getchar();
    xxxxxxxx;
    ========
```

First the **character** is initialized to ' '. The **while** statement then begins by testing whether **character** is not equal to Y. Since the **character** was initialized to ' ', the test is true and the loop statement

```
    character = getchar();
```

is executed. Each time a letter is keyed in, the test is carried out and the loop statement is executed until the letter Y is pressed. When Y is pressed, the condition becomes false because **character** equals Y, and the loop terminates, thus transferring the control to the statement xxxxxxxx;. This is a typical example of sentinel-controlled loops. The character constant 'Y' is called *sentinel* value and the variable **character** is the condition variable, which often referred to as the *sentinel variable*.

# # WORKED-OUT PROBLEM 8.1

A program to evaluate the equation  
$y = x^n$  
when n is a non-negative integer, is given in Fig. 8.2.