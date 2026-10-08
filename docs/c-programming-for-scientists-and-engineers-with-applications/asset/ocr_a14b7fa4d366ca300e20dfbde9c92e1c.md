# 292 Modular Design and Functions

```
int var1, var2, var3, sum;
var1 = 10;
var2 = 20;
var3 = 30;
sum = funcsum(&var1, &var2, &var3); /* passing arguments as addresses */

printf("var1 = %d var2 = %d var3 = %d sum = %d\n",
var1, var2, var3, sum);

return 0;

int funcsum(int *varx, int *vary, int *varz) /* define parameters */
{
    /* specific pointers */
    int sum1;
}
sum1 = *varx + *vary + *varz; /* accessing values through pointers */

return sum1;
```

Output: var1 = 10 var2 = 20 var3 = 30 sum = 60

Figure 5.6 shows the state of variables and their memory address in the main program. The addresses of the variables var1, var2 and var3 are passed as arguments. Since the arguments of the function call in the main program are addresses, the function prototype must declare the parameters as pointer data types. The parameter data types are int *, int *, and int * in the prototype. In the function header the data types must match the data types in the prototype. Therefore the data type of the parameters in the function header is int *, int *, and int *, which matches the data type specified in the prototype.

We have already seen call-by-pointer in the use of standard input functions. When a function is to return a value through the argument list it must be given an address to which it will return the value. We have already seen this with the use of the library input routines. For instance,

```
int a, b, errflg;
...
errflg = scanf("%d %d", &a, &b);
```