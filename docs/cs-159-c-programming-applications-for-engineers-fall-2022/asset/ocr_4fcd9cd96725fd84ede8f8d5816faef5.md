```
Output Generated:
warning: suggest explicit braces to avoid ambiguous 'else'
```

```
Example of dangling else logical error:
int x = 3;
int y = 2;
int z = 0;
if (x == 3)
    if (y != 2)
        z++;
    else
        z--;
printf("z = %d\n", z);
```

# Logic interpretation of code above: