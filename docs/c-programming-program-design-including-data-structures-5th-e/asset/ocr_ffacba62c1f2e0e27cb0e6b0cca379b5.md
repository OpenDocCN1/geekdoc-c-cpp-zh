+   a. `(x < 5) ? y = 10 : y = 20;`
+   
+   b. `(fuel >= 10) ? drive = 150 : drive = 30;`
+   
+   c. `(booksBought >= 3) ? discount = 0.15 : discount = 0.0;`

17. Suppose that you have the following conditional expression. (Assume that all the variables are properly declared.)

```
```cpp
(0 < backyard && backyard <= 5000) ? fertilizingCharges = 40.00
                                  : fertilizingCharges = 40.00 + (backyard - 5000) * 0.01;
```
```

+   a. What is the value of `fertilizingCharges` if the value of `backyard` is 3000?
+   
+   b. What is the value of `fertilizingCharges` if the value of `backyard` is 5000?
+   
+   c. What is the value of `fertilizingCharges` if the value of `backyard` is 6500?

18. State whether the following are valid `switch` statements. If not, explain why. Assume that n and digit are `int` variables.

```
```cpp
switch (n <= 2)
{
case 0:
    cout << "Draw." << endl;
    break;
case 1:
    cout << "Win." << endl;
    break;
case 2:
    cout << "Lose." << endl;
    break;
}
```
```

```
```cpp
switch (digit / 4)
{
case 0,
case 1:
    cout << "low." << endl;
    break;
case 1,
case 2:
    cout << "middle." << endl;
    break;
case 3:
    cout << "high." << endl;
}
```
```

```
```cpp
switch (n % 6)
{
case 1:
case 2:
case 3:
```
```

![](bbox=[0.904, 0.265, 1.0, 0.369])