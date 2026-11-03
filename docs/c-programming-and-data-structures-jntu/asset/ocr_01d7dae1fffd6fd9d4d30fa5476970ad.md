# User-Defined Functions 10.15

```
float principal, inrate;
int period;
printf("Enter principal amount, interest");
printf("rate, and period \n");
scanf("%f %f %d", &principal, &inrate, &period);
printf("\n");
value(principal,inrate,period);
```

```
char ch;
{
int i;
for(i=1; i<=52; i++)
printf("%c",ch);
printf("\n");
}
```

```
value(p,r,n)
{
int n;
float sum;
sum = p;
year = 1;
while(year <= n)
{
sum = sum * (1+rate);
year = year + 1;
}
printf("%f %f %d %f\n", p,r,n,sum);
}
```

Output
Enter principal amount, interest rate, and period
5000 0.12 5
5000.000000 0.120000 5 8811.708984

Fig. 10.7 Functions with arguments but no return values

However, we may not always wish to have the result of a function displayed. We may use it in the calling function for further processing. Moreover, to assure a high degree of portability between programs, a function should generally be coded without involving any I/O operations. For example, different programs may require different output formats for displaying results. These shortcomings can be overcome by handing over the result of a function to its calling function where the returned value can be used as required by the program.