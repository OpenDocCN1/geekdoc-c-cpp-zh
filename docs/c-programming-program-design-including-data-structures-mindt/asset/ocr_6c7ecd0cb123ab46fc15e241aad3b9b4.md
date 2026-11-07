| St. in Line | Value of the Variables | Statement and Effect |
|---|---|---|
| 30 | `main`: `num1 = 10`, `num2 = 31`, `ch = A`; `funTwo`: `x = 25`, `y = 50`, `w = A` | `x++;` Increment the value of x by 1. Because x is the reference parameter and contains the address of `num2`, the value of `num2` is incremented by 1. |
| 31 | `main`: `num1 = 10`, `num2 = 31`, `ch = A`; `funTwo`: `x = 25`, `y = 50`, `w = A` | `y = y * 2;` Multiply the value of y by 2 and store the result in y. |
| 32 | `main`: `num1 = 10`, `num2 = 31`, `ch = G`; `funTwo`: `x = 25`, `y = 50`, `w = G` | `w = 'G';` Store 'G' in w. Because w is the reference parameter and contains the address of ch, the value of ch is updated. |

Line 33 produces the following output:

```
Line 33: Inside funTwo: x = 31, y = 50, and w = G
```

After the statement in Line 33 executes, control goes to Line 16. The memory allocated for the variables of function funTwo is deallocated. The values of the variables of function main are as shown in Figure 6-13.

![](bbox=[0.183, 0.663, 0.909, 0.8])

FIGURE 6-13  Values of the variables after the statement in Line 16

The statement in Line 16 produces the following output:

```
Line 16: After funTwo: num1 = 10, num2 = 31, and ch = G
```

After the statement in Line 16 executes, the program terminates.