The **address-of** operator (also `&`) queries the address of a variable. To get the address of a variable, place a `&` in front of the variable. For example, given the code in Table A.1, the following code outputs the value `0xC234`:

```
std::cout << &y;
```

A **pointer** is a variable that stores an integral value corresponding to a memory address. The following line declares the pointer `p` that stores the memory address of the variable `y`:

```
int* p = &y;
```

The `*` after the type signifies a pointer. Table A.2 shows the pointer `p` in action. Note that, just like any other variable, `p` has both a memory address and a value. But because `p` is a pointer, its value corresponds to the memory address of `y`.

# Table A.2 Variable Storage (with Pointers)

| Code | Variable | Memory Address | Value |
| :--- | :--- | :--- | :--- |
| `int x = 50;` | x | 0xC230 | 50 |
| `int y = 100;` | y | 0xC234 | 100 |
| `int z = 200;` | z | 0xC238 | 200 |