```
```c
main( )
{
    y = 5;
    . . . .
    . . . .
}
int y;          /* global declaration */
func1( )
{
    y = y+1;
}
```
```

We have a problem here. As far as **main** is concerned, y is not defined. So, the compiler will issue an error message. Unlike local variables, global variables are initialized to zero by default. The statement `y = y+1;` in func1 will, therefore, assign 1 to y.

# ### 11.13.3 External Declaration

In the program segment above, the **main** cannot access the variable y as it has been declared after the **main** function. This problem can be solved by declaring the variable with the storage class **extern**.

For example:

```
```c
main( )
{
    extern int y;    /* external declaration */
    . . . .
    . . . .
}
func1( )
{
    extern int y;    /* external declaration */
    . . . .
    . . . .
}
int y;                /* definition */
```
```

Although the variable y has been defined after both the functions, the *external declaration* of y inside the functions informs the compiler that y is an integer type defined somewhere else in the program. Note that **extern** declaration does not allocate storage space for variables. In case of arrays, the definition should include their size as well.

Example:

```
```c
main( )
{    int i;
     void print_out(void);
     extern float height [ ];
     . . . .
}
```
```