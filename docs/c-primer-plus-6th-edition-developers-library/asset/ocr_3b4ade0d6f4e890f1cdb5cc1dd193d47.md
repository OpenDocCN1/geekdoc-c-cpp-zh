# ## `char` Constants

C treats `char` constants as type `int`, and C++ treats them as type `char`. For instance, consider this statement:

```
```c
char ch = 'A';
```
```

In C, the constant `'A'` is stored in an int-sized chunk of memory; more precisely, the character code is stored in the `int`. The same numeric value is also stored in the variable `ch`, but here it occupies just one byte of memory.

C++, on the other hand, uses one byte for `'A'`, as well as for `ch`. This distinction doesn’t affect any of the examples in this text. However, some C programs do make use of char constants being type `int` by using character notation to represent integer values. For instance, if a system has a 4-byte `int`, you can do this in C:

```
```c
int x = 'ABCD';  /* ok in C for 4-byte int but not for C++ */
```
```

The meaning of `'ABCD'` is a 4-byte `int` in which the first byte stores the character code for the letter A, the second byte stores the character code for B, and so on. Note that `'ABCD'` is something quite different from "ABCD". The former is just a funny way of writing an `int` value, but the latter is a string and corresponds to the address of a 5-byte chunk of memory.

Consider the following code:

```
```c
int x = 'ABCD';
char c = 'ABCD';
printf("%d %d %c %c\n", x, 'ABCD', c, 'ABCD');
```
```

On our system, it produces this output:

```
```text
1094861636 1094861636 D D
```
```

This example illustrates that if you treat `'ABCD'` as an `int`, it is a 4-byte integer value, but if you treat it as type char, the program looks only at the final byte. Attempt to print `'ABCD'` by using the `%s` specifier caused the program to crash on our system, because the numeric value of `'ABCD'` (1094861636) was an out-of-bounds address.

The rationale for using values such as `'ABCD'` is that it provides a means to set each byte in the `int` independently, because each character corresponds exactly to one byte. However, a better approach, because it doesn’t depend on particular character codes, is to use hexadecimal values for integer constants, using the fact that each two-digit hexadecimal group corresponds to one byte. Chapter 15, “Bit Fiddling,” discusses this technique. (Early versions of C didn’t provide hexadecimal notation, which probably is why the multicharacter constant technique was developed in the first place.)

# ## The `const` Modifier

In C, a global `const` has external linkage, but in C++, it has internal linkage. That is, the C++ declaration