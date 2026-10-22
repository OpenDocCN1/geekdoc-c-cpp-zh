![](bbox=[0.18, 0.14, 0.78, 0.33])

```
int dates[y], *pti;
pti = dates; (or pti = & dates[0];)
```

pointer variable pti is assigned the address of the first element of the array dates

Figure 10.3 An array and pointer addition.

Now we can define more clearly what is meant by pointer-to-int, pointer-to-float, or pointer-to-any other data object:

+   - The value of a pointer is the address of the object to which it points. How the address is represented internally is hardware dependent. Many computers, including PCs and Macintoshes, are byte addressable, meaning that each byte in memory is numbered sequentially. Here, the address of a large object, such as type double variable, typically is the address of the first byte of the object.
+   - Applying the * operator to a pointer yields the value stored in the pointed-to object.
+   - Adding 1 to the pointer increases its value by the size, in bytes, of the pointed-to type.

As a result of C’s cleverness, we have the following equalities:

```
dates + 2 == &date[2]      // same address
*(dates + 2) == dates[2]    // same value
```

These relationships sum up the close connection between arrays and pointers. They mean that you can use a pointer to identify an individual element of an array and to obtain its value. In essence, we have two different notations for the same thing. Indeed, the C language standard describes array notation in terms of pointers. That is, it defines ar[n] to mean *(ar + n). You can think of the second expression as meaning, “Go to memory location ar, move over n units, and retrieve the value there.”