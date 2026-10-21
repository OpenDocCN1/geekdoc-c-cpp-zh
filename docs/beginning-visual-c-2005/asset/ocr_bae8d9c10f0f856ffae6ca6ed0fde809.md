```
cout << endl;                  // with auto conversion of 2nd parameter
    << "x = " << x;

cout << endl;
return 0;
}

// Function to compute positive integral powers of a double value
// First argument is value, second argument is power index
double power(double x, int n)
{                               // Function body starts here...
    double result = 1.0;            // Result stored here
    for(int i = 1; i <= n; i++)
        result *= x;
    return result;
}                               // ...and ends here
```

This program shows some of the ways in which you can use the function power(), specifying the arguments to the function in a variety of ways. If you run this example, you get the following output:

```
5.0 cubed = 125
3.0 cubed = 27
x = 81
```

# How It Works

After the usual #include statement for input/output and the using declarations, you have the prototype for the function power(). If you were to delete this and try recompiling the program, the compiler wouldn’t be able to process the calls to the function in main() and would instead generate a whole series of error messages:

```
error C3861: 'power': identifier not found
```

and the error message:

```
error C2365: 'power' : redefinition; previous definition was 'formerly unknown identifier'
```

In a change from previous examples, I’ve used the new keyword void in the function main() where the parameter list would usually appear to indicate that no parameters are to be supplied. Previously, I left the parentheses enclosing the parameter list empty, which is also interpreted in C++ as indicating that there are no parameters; but it’s better to specify the fact by using the keyword void. As you saw, the keyword void can also be used as the return type for a function to indicate that no value is returned. If you specify the return type of a function as void, you must not place a value in any return statement within the function; otherwise, you get an error message from the compiler.

You gathered from some of the previous examples that using a function is very simple. To use the function power() to calculate 5.0³ and store the result in a variable y in our example, you have the following statement:

```
y = power(5.0, 3);
```