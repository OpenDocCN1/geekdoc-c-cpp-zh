# # User-Defined Functions 10.17

```
printf("Enter principal amount, interest");
printf(rate, and period\n");
scanf("%f %f", &principal, &inrate);
printf("\n");
amount = value(principal, inrate, period);
printf("\n%5f%5f%5d%5f\n", principal, inrate, period, amount);
printfline("=", 52);
}
/*--------------------------------------*/
```

```
printline(ch,len)
int len;
char ch;
{
int i;
for(i=1;i<=len;i++) printf("%c",ch);
printf("\n");
}
/*--------------------------------------*/
```

```
value(p,r,n)
int n;
float p,r;
{
int year;
float sum;
sum = p; year = 1;
while(year <=n)
{
sum = sum * (1 + r);
year = year + 1;
}
return(sum);
}
/*--------------------------------------*/
```



Enter principal amount, interest rate, and period
5000 0.12 5
5000.000000 0.120000 5 8811.000000

3. The calling statement is executed normally and the returned value is thus assigned to amount. Note that the value returned by the function is only the integer part of sum. Another important change is the inclusion of a second argument to printline function to receive the value of length of the line from the calling function. Thus, the function call printfline("=", 52); will transfer the control to the function printline and assign the following values to the formal arguments ch, and len: