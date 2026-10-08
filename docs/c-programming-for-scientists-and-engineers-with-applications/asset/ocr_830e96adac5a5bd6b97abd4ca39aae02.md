# 296 Modular Design and Functions

```
int funcsum(int *varx, int *vary, int *varz)
{
    int sum;
    sum = *varx + *vary + *varz;
    return sum;
}
```

the variables varx, vary, and varz are dereferenced by placing an asterisk (*) in front of them. The value of pointer varx is an address and its content is *varx, which is, say, 10. The value of pointer vary is an address and its content is *vary, which is, say, 20. Finally, the value of varz is an address and its content is *varz, which is, say, 30. In the assignment statement sum = *varx + *vary + *varz, *varx is replaced by 10, *vary is replaced by 20, and *varz is replaced by 30. The result assigned to the variable sum is 60. The asterisk (*) tells the computer to use the value as an address, find that address, and pick up (or store) the value there.

If the address variable is dereferenced in an output statement, on the right side of an assignment statement, or anywhere a value is needed, the value at that address is picked and used.

```
int x = 14;                   /* 14 is stored at say, address 215390 */
.. func(&x);                  /* function call */
int func(int *addrx)          /* value of addrx is 215390 */
{
    int y;
    printf("%d", *addrx);      /* prints 14 */
    if(*addrx > 0)             /* compares 14 and 0 */
    {
        y = *addrx;               /* assigns the value 14 to y */
        printf("%d", y);         /* prints 14 */
    }
    return 0;
}
```

If the address variable is dereferenced on the left side of an assignment statement or anywhere an address is needed for storing, a value is stored in the storage of the argument in the function call.

```
int x, y;
x = 14;                      /* 14 is stored at say, address 215390 */
y = 27;                      /* 27 is stored at say, address 215394 */
..func(&x, &y);               /* function call */
```