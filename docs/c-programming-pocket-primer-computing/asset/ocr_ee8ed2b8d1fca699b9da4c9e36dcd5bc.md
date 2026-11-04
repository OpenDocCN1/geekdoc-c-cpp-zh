Notice the following: the pointer `p` has been initialized with the address of the variable *x* after the variable *x* has been declared *and initialized* with the value 7.

Another way to achieve the same result is shown in the following snippet:

```
```c
int *p;
int x = 7;
p = &x;
```
```

In the preceding code snippet, `p` is declared as an uninitialized pointer to an integer, and then `x` is initialized as an integer whose value is 7, followed by setting the value of `p` equal to the address of `x` (which is denoted by `&x`).

Keep in mind that assigning values can only be done when data types match. For example, assigning `int x = 7` is valid because the left and right side data types are both `int`.

As another example, declaring and assigning a pointer with `int *p = &x` is valid because the left and right side data types are both `int *`.

As a third example, the declaration `int *p = 1234` is invalid because the left side has the type “pointer to int” and the right side has the type “int.” Even if the types match, you *must also ensure the address assigned to a pointer is a valid address of data in your program*. Based on the preceding statement, we know that the code snippet `int *p=1234` is invalid because of a type error.

On the other hand, the following code snippet is valid because the pointer `p` is initialized with the address of the variable `x` that is declared *before* the pointer `p` is declared and initialized: