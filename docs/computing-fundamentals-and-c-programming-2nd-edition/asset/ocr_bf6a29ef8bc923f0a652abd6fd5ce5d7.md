# # DEBUGGING EXERCISES

+   1. Find errors, if any, in the following function definitions:

LO 11.3

```
(a) void abc (int a, int b)
{
        int c;
        . . . .
        return (c);
}
(b) int abc (int a, int b)
{
        . . . .
        . . . .
}
(c) int abc (int a, int b)
{
        double c = a + b;
        return (c);
}
(d) void abc (void)
{
        . . . .
        . . . .
        return;
}
(e) int abc(void)
{
        . . . .
        . . . .
        return;
}
```

+   2. Find errors in the following function calls:

LO 11.3

```
(a) void xyz ( );
(b) xyz ( void );
(c) xyz ( int x, int y);
(d) xyzz ( );
(e) xyz ( ) + xyz ( );
```

# # PROGRAMMING EXERCISES

+   1. Write a function **exchange** to interchange the values of two variables, say x and y. Illustrate the use of this function, in a calling function. Assume that x and y are defined as global variables.

LO 11.2

+   2. Write a function **space(x)** that can be used to provide a space of x positions between two output numbers. Demonstrate its application.

LO 11.6

+   3. Use recursive function calls to evaluate
+   
+       f(x) = x - x^3/3! + x^5/5! - x^7/7! + ...

LO 11.4