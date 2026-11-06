![](bbox=[0.245, 0.093, 0.89, 0.46])

• The parameter variable `side_length` of the `cube_volume` function is created. ❶
• The parameter variable is initialized with the value of the argument that was passed in the call. In our case, `side_length` is set to 2. ❷
• The function computes the expression `side_length * side_length * side_length`, which has the value 8. That value is stored in the variable `volume`. ❸
• The function returns. All of its variables are removed. The return value is transferred to the caller, that is, the function calling the `cube_volume` function. ❹

Now consider what happens in a subsequent call `cube_volume(10)`. A new parameter variable is created. (Recall that the previous parameter variable was removed when the first call to `cube_volume` returned.) It is initialized with the argument 10, and the process repeats. After the second function call is complete, its variables are again removed.

Like any other variables, parameter variables can only be set to values of compatible types. For example, the `side_length` parameter variable of the `cube_volume` function has type double. It is valid to call `cube_volume(2.0)` or `cube_volume(2)`. In the latter call, the integer 2 is automatically converted to the double value 2.0. However, a call `cube_volume("two")` is not legal.

![](bbox=[0.079, 0.819, 0.194, 0.905])

# SELF-CHECK 10.

What does this program print? Use a diagram like Figure 3 to find the answer.

```
```cpp
double mystery(int x, int y)
{
    double z = x + y;
    z = z / 2.0;
}
```
```