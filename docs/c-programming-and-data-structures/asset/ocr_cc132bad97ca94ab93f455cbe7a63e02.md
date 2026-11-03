where *type-name* is one of the standard C data types. The expression may be a constant, variable or an expression. Some examples of casts and their actions are shown in Table 1.24.

# Table 1.24 Use of Casts

| Example | Action |
|---|---|
| x = (int) 7.5 | 7.5 is converted to integer by truncation. |
| a = (int) 21.3/(int)4.5 | Evaluated as 21/4 and the result would be 5. |
| b = (double)sum/n | Division is done in floating point mode. |
| y = (int) (a+b) | The result of a+b is converted to integer. |
| z = (int)a+b | a is converted to integer and then added to b. |
| p = cos((double)x) | Converts x to double before using it. |

Casting can be used to round-off a given value. Consider the following statement:

x = (int) (y+0.5);

If y is 27.6, y+0.5 is 28.1 and on casting, the result becomes 28, the value that is assigned to x. Of course, the expression, being cast is not changed.

# EXAMPLE 1.39 Figure 1.94 shows a program using a cast to evaluate the equation SUM = Σ_{i=1}^{n} (1/i)

```
Program
main()
{
    float sum ;
    int n ;
    sum = 0 ;
    for( n = 1 ; n <= 10 ; ++n )
    {
        sum = sum + 1/(float)n ;
        printf("%2d %6.4f\n", n, sum) ;
    }
}

Output
1 1.0000
2 1.5000
3 1.8333
4 2.0833
5 2.2833
6 2.4500
7 2.5929
8 2.7179
9 2.8290
10 2.9290
```