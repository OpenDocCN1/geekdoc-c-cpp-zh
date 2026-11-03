4. Now, in the main function block, output the result of both postfix and prefix increment operations

```
printf("Postfix increment: %d\n", c++);
printf("Postfix now: %d\n", c);
printf("Prefix increment: %d\n", ++d);
printf("Prefix now: %d\n", d);
```

5. At the end of the main function block, return a zero integer value, as required by the function declaration

```
return 0;
```

6. Save the program file, then compile and execute the program to see the results of the arithmetical operations

```
Addition: 12
Subtraction: 4
Multiplication: 32
Division: 2
Modulus: 4
Postfix increment: 1
Postfix now: 2
Prefix increment: 2
Prefix now: 2
```

Notice that the variable value is immediately increased only with the prefix increment operator – with the postfix operator it is incremented the next time it is referenced.