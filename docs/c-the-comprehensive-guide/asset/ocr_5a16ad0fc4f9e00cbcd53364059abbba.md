However, for each type, there is a corresponding additional type that represents not the value itself, but the address of a value of that type. For example, if you define a variable `int value = 42;`, then `value` has the type `int`. The address of `value` has the type `int*`. You can now define a new variable of this additional type that holds the address of `value`:

```
```cpp
int value = 42;
int* pValue = &value;
```
```

In Figure 20.1, you can see how this looks in memory.

![](bbox=[0.143, 0.284, 0.417, 0.455])

**Figure 20.1** You can think of memory locations as houses on a street.

The definition of `pValue` in the second line requires an explanation. Because `pValue` is not an `int`, `int* pValue = value;` would be incorrect; you do not need the *value* from `value`, but its *address*. And this is exactly what the *unary address operator* `&` before the variable name does. `&value` gives you the address of `value`. Because `value` is of type `int`, `&value` is of type `int*`. The assignment of `&value` to `int* pValue` is therefore correct.

# 20.2 Pointer

The exciting thing now is that with `*pValue` you have an alternative way to access the value in `value`. When you apply the *unary dereference operator* `*` to `pValue`, it points to the memory with the 42. If you write something there, you also change the value of `value`. With `*pValue`, you have an *alias* for `value`:

```
```cpp
*pValue = 18;
cout << value << "\n"; // Output: 18
```
```

If I may stick with the image of the street and the houses, the following happens: With `pValue` you go to its house (`0xab02`), look inside, and find the address `0xab04`. With the dereference operator `*` you follow the arrow and arrive at the house of `value`. The assignment `= 18` writes the new value to the location in memory—that is, at `value`.