```
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

Output

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