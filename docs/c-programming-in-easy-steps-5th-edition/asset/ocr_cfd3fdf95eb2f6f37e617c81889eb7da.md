```
```cpp
void computeTriple( int& value )
{
    value *= 3;    // Multiply and assign a referenced value.
}
```
```

+   7. In the main function, pass a reference argument to a function to output the variable value to which it refers

```
```cpp
writeOutput( ref );
```
```

+   8. Next, use the reference to increase the variable value, then display its new value

```
```cpp
ref += 15;    // Add and assign a referenced value.
writeOutput( ref );
```
```

+   9. Now, pass a reference argument to a function to multiply the variable to which it refers, then display its new value

```
```cpp
computeTriple( ref );
writeOutput( ref );
```
```

+   10. Save, compile, and run the program to see the computed values output

![](bbox=[0.3, 0.318, 0.7, 0.409])

![](bbox=[0.118, 0.42, 0.207, 0.482])

The function prototype and definition must both contain a reference argument.

![](bbox=[0.118, 0.512, 0.207, 0.573])

Functions that operate directly on variables within the calling function need no **return** statement.