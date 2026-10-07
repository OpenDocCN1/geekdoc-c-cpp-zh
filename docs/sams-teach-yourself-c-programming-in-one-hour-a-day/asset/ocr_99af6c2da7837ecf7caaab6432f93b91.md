# LESSON 12 Understanding Variable Scope

```
17: void funcl(void)
18: {
19:     static int x;
20:     int y;
21:
22: printf("x = %d, y = %d\n", x++, y++);
23: }
```

When you run the modified program, you might find that the value of y increases
1 with each iteration. This means that y keeps its value between calls to the function
even if it is an automatic local variable. What you've read here about automatic
variables losing their value a bunch of malarkey?

No, what you read is true. (Have faith!) If you find that an automatic variable keeps its
value during repeated calls to the function, it is only by chance. Here is what happens:
Each time the function is called, a new y is created. The compiler might use the same
memory location for the y that was not explicitly initialized by the function, the storage location might contain
the value that y had during the preceding call. The variable seems to have kept its old
value, but it's just a chance occurrence; you can't count on it happening every
time. Because you can't count on it, you should never count on it!

Because automatic is the default for local variables, it doesn't need to be specified in the
variable definition. If you want to, you can include the auto keyword in the definition
before the type keyword, as shown here:

```
void funcl(int y)
{
    auto int count;
    /* Additional code goes here */
}
```

# The Scope of Function Parameters

A variable that is contained in a function's parameter list has local scope. For
example, look at the following function:

```
void funcl(int x)
{
    int y;
    /* Additional code goes here */
}
```

Both x and y are local variables with a scope that is the entire function funcl(). Of
course, it initially contains whatever value was passed to the function by the calling
program. After you make use of that value, you can use x like any other local variable.