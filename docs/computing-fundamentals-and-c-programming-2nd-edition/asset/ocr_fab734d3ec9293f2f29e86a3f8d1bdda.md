As pointed out earlier, a function that does not return any value cannot be used in an expression. It can only be used as an independent statement.

# # WORKED-OUT PROBLEM 11.1

Write a program with multiple functions that do not communicate any data between them.

A program with three user-defined functions is given in Fig. 11.4. **main** is the calling function that calls **println** and **value** functions. Since both the called functions contain no arguments, there are no argument declarations. The **println** function, when encountered, prints a line with a length of 35 characters as prescribed in the function. The **value** function calculates the value of principal amount after a certain period of years and prints the results. The following equation is evaluated repeatedly:

**value = principal(1+interest-rate)**

```
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
```

**Levels of Difficulty**
L: Low; M: Medium; H: High