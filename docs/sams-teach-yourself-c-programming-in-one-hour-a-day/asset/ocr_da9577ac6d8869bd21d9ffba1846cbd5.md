# Calling Functions

The second method can be used only with functions that have a return value. Because these functions evaluate to a value (that is, their return value), they are valid C expressions and can be used anywhere a C expression can be. You've already seen an expression with a return value used as the right side of an assignment statement. Here are some examples.

In the following example, half_of() is a parameter of a function:

```
printf("Half of %d is %d", x, half_of(x));
```

The first function, half_of() is called with the value of x, and then printf() is called using the values "Half of %d is %d", x, and half_of(x).

In this example, multiple functions are used in the expression:

```
y = half_of(x) + half_of(z);
```

Although half_of() is used, the code shows the same statement, but not all on one line:

```
a = half_of(x);
b = half_of(z);
y = a + b;
```

The following two examples show effective ways to use the return values of functions. Here, a function is used with the if statement:

```
if ( half_of(x) > 10 )
{
    /* statements; */
    /* these could be any statements! */
}
```

If the return value of the function meets the criteria (in this case, half_of() returns a value greater than 10), the if statement is true, and its statements are executed. If the returned value does not meet the criteria, the statements in the if block are not executed.

The following example is even better:

```
if ( do_process() != OKAY )
{
    /* statements; */
    /* do error routine */
}
```

Again, actual statements are not provided, nor is do_process() a real function; however, this is an important example. The return value of a process is checked to see whether it ran correctly. If it didn't, the statements take care of any error handling or cleanup. This is commonly used with accessing information in files, comparing values, and allocating memory.