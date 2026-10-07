```
result = gcd (150, 35);
NSLog("*@The gcd of 150 and 35 is %i", result);
```

```
result = gcd (1026, 405);
NSLog("*@The gcd of 1026 and 405 is %i", result);
```

```
NSLog("*@The gcd of 83 and 240 is %i", gcd (83, 240);
pool drain];
return 0;
```

# Program 13.5 Output

The gcd of 150 and 35 is 5
The gcd of 1026 and 405 is 27
The gcd of 83 and 240 is 1

The function gcd is defined to take two integer arguments. The function refers to these arguments through their formal parameter names: u and v. After declaring the variable to be of int, the program displays the values of the arguments u and v, together with an appropriate message at the terminal. The function then calculates and returns the greatest common divisor of the two integers.

The statement

```
result = gcd (150, 35);
```

says to call the function gcd with the arguments 150 and 35, and to store the value of this function in the variable result.

If the return type declaration for a function is omitted, the compiler assumes that the function will return an integer—default. Many programmers take advantage of this fact and omit the return type declaration for functions that return integers. However, this is a bad programming habit that you should avoid. The compiler will warn you that the return type defaults to int, which is an indication that you’re doing something wrong!

The default return type for functions differs from that for methods. Recall that, if no return type is specified for a method, the compiler assumes it returns a value of type id. Again, you should always declare the return type for a method instead of relying on this fact.

# Declaring Return Types and Argument Types

We mentioned earlier that the Objective-C compiler assumes that a function returns a value of type int as the default case. More specifically, whenever a call is made to a function, the compiler assumes the function returns a value of type int unless either of the following has occurred: