# # 5.16 Computer Programming

```
```c
main()
{
    float principal, inrate, amount;
    int period;
    printf("Enter principal amount, interest rate, and period\n");
    printf("rate %f %d, &period\n");
    scanf("%f %f %d", &principal, &inrate, &period);
    println ("* * * ", 52);
    amount = value (principal, inrate, period);
    printf("\n%s%f\t%d\t%d\t%f\n", principal,
    inrate,period,amount);
    println("* * * ",52);
}
```
```

```
```c
void println(char ch, int len)
{
    int i;
    for (i=1;i<=len;++i) printf("%c",ch);
    printf("\n");
}
```
```

```
```c
value(float p, float r, int n) /* default return type */
{
    int year;
    float sum;
    year = 1;
    while(year <=n)
    {
        sum = sum * (1+r);
        year = year +1;
    }
    return(sum); /* returns int part of sum */
}
```
```

Output

```
```
Enter principal amount, interest rate, and period
5000 0.12 5
**********************
5000.000000 0.120000 5 8811.000000
**********************
```
```

# Fig. 9 Functions with arguments and return values

The calculated value is passed to main through statement:
return(sum);

Since, by default, the return type of value function is int, the 'integer' value of sum at this point is returned to main and assigned to the variable amount by the functional call:
amount = value (principal, inrate, period);

The following events occur, in order, when the above function call is executed:

+   1. The function call transfers the control along with copies of the values of the actual arguments to the function where the formal arguments p, r, and n are assigned the actual values of principal, inrate and period respectively.