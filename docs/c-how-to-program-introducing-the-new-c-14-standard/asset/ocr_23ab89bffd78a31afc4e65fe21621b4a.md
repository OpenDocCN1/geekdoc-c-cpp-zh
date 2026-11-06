the initializer list. For example,

```
```cpp
int n[] {50, 20, 30, 10, 40};
```
```

creates a five-element `array`.

![](bbox=[0.118, 0.331, 0.19, 0.386])

# Error-Prevention Tip 8.3

> *Always specify a built-in array’s size, even when providing an initializer list. This enables the compiler to generate an error message if there are more initializers than array elements.*

# 8.5.3 Passing Built-In Arrays to Functions

The value of a built-in array’s name is implicitly convertible to the address of the built-in array’s first element. So `arrayName` is implicitly convertible to `&arrayName[0]`. For this reason, you don’t need to take the address (`&`) of a built-in array to pass it to a function—you simply pass the built-in array’s name. As you saw in **Section 8.4**, a function that receives a pointer to a variable in the caller can *modify* that variable in the caller. For built-in arrays, this means that the called