+   8. Next, use the pointer to increase the variable value, then display its new value

```
    *ptr += 15;    // Add and assign a dereferenced value.
    writeOutput( ptr );
```

+   9. Now, pass a pointer argument to a function to multiply the variable to which it points, then display its new value

```
    computeTriple( ptr );
    writeOutput( ptr );
```

+   10. Save, compile, and run the program to see the computed values output

![](bbox=[0.265, 0.21, 0.735, 0.319])

![](bbox=[0.118, 0.326, 0.189, 0.377])

The function prototype and definition must both contain a pointer argument.

![](bbox=[0.118, 0.41, 0.189, 0.461])

Functions that operate directly on variables within the calling function need no **return** statement.