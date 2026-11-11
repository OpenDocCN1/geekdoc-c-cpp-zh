**Table 2.2: Continued**

| Format specifier | Description | Example | Output |
|---|---|---|---|
| `%x` | `%x` is used to print the hexadecimal equivalent of an integer | `int v=320;`<br>`printf("Value is %x",v);`<br>`/*This prints 140 which is an hexadecimal equivalent of decimal value 320*/` | `Value is 140` |
| `%e` | `%e` is used to print a value of floating point variable in exponential format with lower case e appearing in the output | `float v=32000.9;`<br>`printf("Value is %e",v);` | `Value is 3.200090e+004` |
| `%E` | `%E` is used to print a value of floating point variable in exponential format with lower case e appearing in the output | `float v = 32000.9;`<br>`printf("Value is %E",v);` | `Value is 3.200090E+004` |
| `%lf` | `%lf` is used to print a value of double variable in a decimal form | `double v = 320001200.9;`<br>`printf("Value is %lf",v);` | `Value is 320001200.900002` |
| `%le` | `%le` is used to print a value of double variable in exponential format with lower case e appearing in the output | `double v = 320001200.9;`<br>`printf("Value is %le",v);` | `Value is 3.200012e+008` |
| `%lE` | `%lE` is used to print a value of double variable in exponential format with upper case E appearing in the output | `double v = 320001200.9;`<br>`printf("Value is %lE",v);` | `Value is 3.200012E+008` |

Let us assume that there is another variable y as shown below,

```
int y=5;
```

If we need to print the value of both x and y in the message as shown in Figure 2.20. then, we need to write the printf statement as shown below

![](bbox=[0.511, 0.77, 0.857, 0.861])

```
printf("There are %d students and %d professors",x,y);
```