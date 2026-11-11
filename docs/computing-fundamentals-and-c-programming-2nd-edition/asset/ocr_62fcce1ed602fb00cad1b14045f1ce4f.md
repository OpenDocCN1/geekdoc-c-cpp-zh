The process of such a local conversion is known as *explicit conversion* or *casting a value*. The general form of a cast is:

```
```c
(type-name) expression
```
```

where *type-name* is one of the standard C data types. The expression may be a constant, variable or an expression. Some examples of casts and their actions are shown in Table 5.7.

**Table 5.7** Use of Casts

| Example | Action |
| --- | --- |
| x = (int) 7.5 | 7.5 is converted to integer by truncation. |
| a = (int) 21.3/(int)4.5 | Evaluated as 21/4 and the result would be 5. |
| b = (double)sum/n | Division is done in floating point mode. |
| y = (int) (a+b) | The result of a+b is converted to integer. |
| z = (int)a+b | a is converted to integer and then added to b. |
| p = cos((double)x) | Converts x to double before using it. |

Casting can be used to round-off a given value. Consider the following statement:

```
```c
x = (int) (y+0.5);
```
```

If y is 27.6, y+0.5 is 28.1 and on casting, the result becomes 28, the value that is assigned to x. Of course, the expression, being cast is not changed.

# WORKED-OUT PROBLEM 5.7

Figure 5.9 shows a program using a cast to evaluate the equation

$$\sum_{i=1}^{N} (1/i)$$

```
```c
Program

        main()
        {
            float    sum ;
            int      n ;
            sum = 0 ;
            for( n = 1 ; n <= 10 ; ++n )
            {
                sum = sum + 1/(float)n ;
                printf("%2d %6.4f\n", n, sum) ;
            }
        }

Output

        1   1.0000
```
```