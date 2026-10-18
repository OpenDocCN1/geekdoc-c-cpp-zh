```
```cpp
return 0;
}
```
```

The output of Program 10.5 would be:

Precision set to 3 digits

| VALUE | SQRT_OF_VALUE |
|---:|---:|
| 1 | 1 |
| 2 | 1.41 |
| 3 | 1.73 |
| 4 | 2 |
| 5 | 2.24 |

Precision set to 5 digits
sqrt(10) = 3.1623
sqrt(10) = 3.162278  (default setting)

> 🡪 **NOTE:** *Observe the following from the output:*
> 
> 1. *The output is rounded to the nearest cent (i.e., 1.6666 will be 1.67 for two digit precision but 1.3333 will be 1.33).*  
> 2. *Trailing zeros are truncated.*  
> 3. *Precision setting stays in effect until it is reset.*  
> 4. *Default precision is 6 digits.*

Program 10.6 shows another program demonstrating the functionality of width and precision manipulators: