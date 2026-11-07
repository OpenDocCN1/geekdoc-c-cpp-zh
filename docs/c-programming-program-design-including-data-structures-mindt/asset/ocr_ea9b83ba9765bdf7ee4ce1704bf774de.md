![](bbox=[0.183, 0.076, 0.909, 0.225])

FIGURE 6-10  Values of the variables just before the statement in Line 22 executes

The following shows how the variables are manipulated after each statement from Lines 22 to 25 executes

| St. # in Line | Value of the Variables | Statement and Effect |
|---|---|---|
| 22 | **main**: `num1 = 10`, `num2 = 15`, `ch = 'A'`<br>**funOne**: `a = 10`, `b` references `num2`, `v = 'A'`, `one = 10` | `one = a;`<br>Copy the value of `a` into `one`. |
| 23 | **main**: `num1 = 10`, `num2 = 15`, `ch = 'A'`<br>**funOne**: `a = 11`, `b` references `num2`, `v = 'A'`, `one = 10` | `a++;`<br>Increment the value of `a` by 1. |
| 24 | **main**: `num1 = 10`, `num2 = 30`, `ch = 'A'`<br>**funOne**: `a = 11`, `b` references `num2`, `v = 'A'`, `one = 10` | `b = b * 2;`<br>Multiply the value of `b` by 2 and store the result in `b`. Because `b` is the reference parameter and contains the address of `num2`, the value of `num2` is updated. |
| 25 | **main**: `num1 = 10`, `num2 = 30`, `ch = 'A'`<br>**funOne**: `a = 11`, `b` references `num2`, `v = 'B'`, `one = 10` | `v = 'B';`<br>Store `'B'` into `v`. |