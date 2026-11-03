```
/* Function2: value() */
void value(void) /* contains no arguments */
{
    int year, period;
    float inrate, sum, principal;
    printf("Principal amount?");
    scanf("%f", &principal);
    printf("Interest rate? ");
    scanf("%f", &inrate);
    printf("Period? ");
    scanf("%d", &period);

    sum = principal;
    year = 1;
    while(year <= period)
    {
        sum = sum * (1+inrate);
        year = year +1;
    }
    printf("\n%8.2f %5.2f %5d %12.2f\n", principal, inrate, period, sum);
}
```

Output

-----------------------------
Principal amount? 5000
Interest rate? 0.12
Period? 5

5000.00 0.12 5 8811.71

-----------------------------

# Fig. 5.4 Functions with no arguments and no return values

It is important to note that the function value receives its data directly from the terminal. The input data include principal amount, interest rate and the period for which the final value is to be calculated. The while loop calculates the final value and the results are printed by the library function printf. When the closing brace of value() is reached, the control is transferred back to the calling function main. Since everything is done by the value itself there is in fact nothing left to be sent back to the called function. Return types of both println and value are declared as void.

Note that no return statement is employed. When there is nothing to be returned, the return statement is optional. The closing brace of the function signals the end of execution of the function, thus returning the control, back to the calling function.

# 5.11 ARGUMENTS BUT NO RETURN VALUES

In Fig. 5.4 the main function has no control over the way the functions receive input data. For example, the function println will print the same line each time it is called. Same is the case with the function value. We could make the calling function to read data from the terminal and pass it on to the called function. This approach seems to be wiser because the calling function can check for the validity of data, if necessary, before it is handed over to the called function.