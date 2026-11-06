![](bbox=[0.11, 0.091, 0.89, 0.33])

# Figure 2  Pointer Variables Can be on Either Side of an Assignment

An expression such as `*account_pointer` can be on the left or the right of an assignment. When it occurs on the left, then the value on the right is stored in the location to which the pointer refers. When it occurs on the right, then the value is fetched from the location and assigned to the variable on the left. For example, the following statement reads the variable to which `account_pointer` currently points, and places its contents into the `balance` variable:

```
```cpp
balance = *account_pointer;
```
```

You can have `*account_pointer` on both sides of an assignment. The following statement withdraws $100:

```
```cpp
*account_pointer = *account_pointer - 100;
```
```

Table 1 contains additional pointer examples.

# Syntax 7.1  Pointer Syntax

![](bbox=[0.245, 0.628, 0.89, 0.924])