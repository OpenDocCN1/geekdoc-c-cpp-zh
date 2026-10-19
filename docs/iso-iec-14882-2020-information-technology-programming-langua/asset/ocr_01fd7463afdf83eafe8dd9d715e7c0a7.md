```
int pcount() const;
```

**Effects:** If the next pointer for the output sequence, `pnext`, is a null pointer, returns zero. Otherwise, returns the current effective length of the array object as the next pointer minus the beginning pointer for the output sequence, `pnext - pbeg`.

# D.13.2.4  `strstreambuf` overridden virtual functions

```
int_type overflow(int_type c = EOF) override;
```

**1  Effects:** Appends the character designated by `c` to the output sequence, if possible, in one of two ways:

+   1. If `c != EOF` and if either the output sequence has a write position available or the function makes a write position available (as described below), assigns `c` to `*pnext++`.\n\n   Returns `(unsigned char)c`.

+   2. If `c == EOF`, there is no character to append.\n\n   Returns a value other than `EOF`.

**2** Returns `EOF` to indicate failure.

**3  Remarks:** The function can alter the number of write positions available as a result of any call.

**4** To make a write position available, the function reallocates (or initially allocates) an array object with a sufficient number of elements `n` to hold the current array object (if any), plus at least one additional write position. How many additional write positions are made available is otherwise unspecified. If `palloc` is not a null pointer, the function calls `(*palloc)(n)` to allocate the new dynamic array object. Otherwise, it evaluates the expression `new charT[n]`. In either case, if the allocation fails, the function returns `EOF`. Otherwise, it sets `allocated` in `strmode`.

**5** To free a previously existing dynamic array object whose first element address is `p`: If `pfree` is not a null pointer, the function calls `(*pfree)(p)`. Otherwise, it evaluates the expression `delete[] p`.

**6** If `(strmode & dynamic) == 0`, or if `(strmode & frozen) != 0`, the function cannot extend the array (reallocate it with greater length) to make a write position available.

**7  Recommended practice:** An implementation should consider `alsize` in making the decision how many additional write positions to make available.

```
int_type pbackfail(int_type c = EOF) override;
```

**8** Puts back the character designated by `c` to the input sequence, if possible, in one of three ways:

+   1. If `c != EOF`, if the input sequence has a putback position available, and if `(char)c == gnext[-1]`, assigns `gnext - 1` to `gnext`.\n\n   Returns `c`.

+   2. If `c != EOF`, if the input sequence has a putback position available, and if `strmode & constant` is zero, assigns `c` to `*--gnext`.\n\n   Returns `c`.

+   3. If `c == EOF` and if the input sequence has a putback position available, assigns `gnext - 1` to `gnext`.\n\n   Returns a value other than `EOF`.

**9** Returns `EOF` to indicate failure.

**10  Remarks:** If the function can succeed in more than one of these ways, it is unspecified which way is chosen. The function can alter the number of putback positions available as a result of any call.

```
int_type underflow() override;
```

**11  Effects:** Reads a character from the *input sequence*, if possible, without moving the stream position past it, as follows:

+   1. If the input sequence has a read position available, the function signals success by returning `(unsigned char)*gnext`.