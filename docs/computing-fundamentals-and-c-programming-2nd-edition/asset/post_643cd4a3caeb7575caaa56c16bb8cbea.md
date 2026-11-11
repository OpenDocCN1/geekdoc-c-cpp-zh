
The function call sends two integer values 10 and 5 to the function.

```c
int mul (int x, int y)
```

which are assigned to x and y respectively. The function computes the product of x and y, assigns the result to the local variable p, and then returns the value 25 to the main where it is assigned to y again.

There are many different ways to call a function. Listed below are some of the ways the function mul can be invoked.

```c
mul (10, 5)
mul (m, 5)
mul (10, n)
mul (m, n)
mul (m + 5, 10)
mul (10, mul(m,n))
mul (expression1, expression2)
```

Note that the sixth call uses its own call as one of the parameters. When we use expressions, they should be evaluated to single values that can be passed as actual parameters.

A function which returns a value can be used in expressions like any other variable. Each of the following statements is valid:

```c
printf("%d\n", mul(p,q));
y = mul(p,q) / (p+q);
if (mul(m,n)>total) printf("large");
```

However, a function cannot be used on the right side of an assignment statement. For instance,

```c
mul(a,b) = 15;
```

is invalid.

A function that does not return any value may not be used in expressions; but can be called to perform certain tasks specified in the function. The function printline() discussed in Section 11.3 belongs to this category. Such functions may be called by simply stating their names as independent statements.

Example:

```c
main( )
{
    printline( );
}
```

Note the presence of a semicolon at the end.

### 11.7.1 Function Call

A function call is a postfix expression. The operator () is at a very high level of precedence (see Table 5.8). Therefore, when a function call is used as a part of an expression, it will be evaluated first, unless parentheses are used to change the order of precedence.

In a function call, the function name is the operand and the parentheses set () which contains the actual parameters is the operator. The actual parameters must match the function's formal parameters in type, order and number. Multiple actual parameters must be separated by commas.

**Note**
- *If the actual parameters are more than the formal parameters, the extra actual arguments will be discarded.*
- *On the other hand, if the actuals are less than the formals, the unmatched formal arguments will be initialized to some garbage.*
- *Any mismatch in data types may also result in some garbage values.*

As pointed out earlier, a function that does not return any value cannot be used in an expression. It can only be used as an independent statement.

## WORKED-OUT PROBLEM 11.1

Write a program with multiple functions that do not communicate any data between them.

A program with three user-defined functions is given in Fig. 11.4. **main** is the calling function that calls **println** and **value** functions. Since both the called functions contain no arguments, there are no argument declarations. The **println** function, when encountered, prints a line with a length of 35 characters as prescribed in the function. The **value** function calculates the value of principal amount after a certain period of years and prints the results. The following equation is evaluated repeatedly:

**value = principal(1+interest-rate)**

```c
/* Function declaration */
void println (void);
void value (void);
main()
{
        println();
        value();
        println();
}
/*        Function1: println( )        */

void println(void)   /* contains no arguments */
{
        int i ;

        for(i=1; i <= 35; i++)
                printf("%c",'-');
        printf("\n");
}
/*        Function2: value( )          */
void value(void)      /* contains no arguments */
{
        int    year, period;
        float  intrate, sum, principal;

        printf("Principal amount?");
        scanf("%f", &principal);
        printf("Interest rate? ");
```

**Levels of Difficulty** L: Low; M: Medium; H: High

![](img/11b034a94fc590add0a7808250a38792_400_0.png)

Fig. 11.5  *One-way data communication*

We shall modify the definition of both the called functions to include arguments as follows:

`void printline(char ch)`

`void value(float p, float r, int n)`

The arguments **ch, p, r,** and **n** are called the *formal arguments*. The calling function can now send values to these arguments using function calls containing appropriate arguments. For example, the function call

`value(500,0.12,5)`

would send the values 500, 0.12 and 5 to the function

`void value( float p, float r, int n)`

and assign 500 to **p**, 0.12 to **r** and 5 to **n**. The values 500, 0.12, and 5 are the *actual arguments*, which become the values of the *formal arguments* inside the called function.

The *actual* and *formal* arguments should match in number, type, and order. The values of actual arguments are assigned to the formal arguments on a *one to one* basis, starting with the first argument as shown in Fig. 11.6.

![](img/11b034a94fc590add0a7808250a38792_400_1.png)

Fig. 11.6  *Arguments matching between the function call and the called function*

We should ensure that the function call has matching arguments. In case, the actual arguments are more than the formal arguments (m > n), the extra actual arguments are discarded. On the other hand, if the actual arguments are less than the formal arguments, the unmatched formal arguments are initialized to some garbage values. Any mismatch in data type may also result in passing of garbage values. Remember, no error message will be generated.

While the formal arguments must be valid variable names, the actual arguments may be variable names, expressions, or constants. The variables used in actual arguments must be assigned values before the function call is made.

Remember that, when a function call is made, only a copy of the values of actual arguments is passed into the called function. What occurs inside the function will have no effect on the variables used in the actual argument list.

## WORKED-OUT PROBLEM 11.2

Modify the program of Program 11.1 to include the arguments in the function calls.

The modified program with function arguments is presented in Fig. 11.7. Most of the program is identical to the program in Fig. 11.4. The input prompt and **scanf** assignment statement have been moved from **value** function to **main**. The variables *principal*, *inrate*, and *period* are declared in **main** because they are used in **main** to receive data. The function call

```c
value(principal, inrate, period);
```

passes information it contains to the function **value**.

The function header of **value** has three formal arguments **p**, **r**, and **n** which correspond to the actual arguments in the function call, namely, **principal**, **inrate**, and **period**. On execution of the function call, the values of the actual arguments are assigned to the corresponding formal arguments. In fact, the following assignments are accomplished across the function boundaries:

```c
p = principal;
r = inrate;
n = period;
```

**Program**

```c
/* prototypes */
void printline (char c);
void value (float, float, int);

main( )
{
    float principal, inrate;
    int period;

    printf("Enter principal amount, interest");
    printf(" rate, and period \n");
    scanf("%f %f %d", &principal, &inrate, &period);
    printline('Z');
    value(principal,inrate,period);
    printline('C');
}
void printline(char ch)
{
    int i ;
    for(i=1; i <= 52; i++)
        printf("%c",ch);
    printf("\n");
}
void value(float p, float r, int n)
{
    int year ;
    float sum ;
    sum = p ;
    year = 1;
    while(year <= n)
    {
        sum = sum * (1+r);
        year = year +1;
    }
    printf("%f\t%f\t%d\t%f\n",p,r,n,sum);
}
```

**Output**

```text
Enter principal amount, interest rate, and period
5000 0.12 5
ZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZ
5000.000000      0.120000        5       8811.708984
CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
```

Fig. 11.7 Functions with arguments but no return values

The variables declared inside a function are known as *local variables* and therefore their values are local to the function and cannot be accessed by any other function. We shall discuss more about this later in the chapter.

The function **value** calculates the final amount for a given period and prints the results as before. Control is transferred back on reaching the closing brace of the function. Note that the function does not return any value.

The function **printline** is called twice. The first call passes the character 'Z', while the second passes the character 'C' to the function. These are assigned to the formal argument **ch** for printing lines (see the output).
