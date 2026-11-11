# Output

```
Before call a=10
After call a=10
```

To understand the working of ‘call by value’ in detail, let us go through the above code line by line. The execution of code will start from the `main()` function. The following table explains the execution of each line in `main()`.

| Statement | Description |
|---|---|
| `int a=10;` | This statement creates a local variable `a` initialized to value 10. Note that, this is a local variable of `main()` and cannot be directly accessed by function `f1()`. |
| `printf ("Before call a=%d\\n",a);` | The statement prints the value of variable `a` which is 10. Hence, the following message is printed on the computer screen:<br><br>`Before call a=10` |
| `f1(a);` | This statement is a function call to `f1()` by passing a value of variable `a` as an argument to the function. On executing this statement, the control is transferred to the function definition of `f1()`, triggering its execution.<br><br>The value 10 is assigned to the formal argument `p` which is the local variable of `f1()` as shown in Figure 8.9. It is important to understand that, there are two variables being created in the memory, first is the variable `a` which is the local variable of `main()` function and the second is the variable `p` which is the local variable of function `f1()`.<br><br>Initially both the variables have same value which is 10 as shown in Figure 8.9. Inside the body of function `f1()`, the statement `p++` changes the value of `p` to 11. After the function completes its execution, the control is transferred back to the `main()` function. |
| `printf ("After call a=%d\\n",a);` | The statement prints the value of variable `a` after execution of the `f1()` is completed. Note that the function `f1()` never changed the value of variable `a` but it had just changed the value of variable `p`. As shown in Figure 8.9 the variables `a` and `p` are two different variables in memory and changing the value of variable `p` will not change the value of variable `a` in any way. When the control returns to the `main()` function the value of variable `a` is still 10. Hence, this statement prints the following message on the computer screen:<br><br>`After call a=10` |

> **NOTES**
> 
> **Call by value** creates two different variables one in the **calling** function, and the other in the **called** function. Updating the value of variable in **called** function will never update the corresponding variable in the **calling** function. This is because the two variables reside at different physical locations in memory.