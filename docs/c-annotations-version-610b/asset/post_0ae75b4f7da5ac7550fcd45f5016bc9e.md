
Sometimes functions explicitly require `unsigned int` to be used. E.g., on AMD architectures the X Window function `XQueryPointer` explicitly requires a pointer to an `unsigned int` variable as one of its arguments. In such situations a pointer to a `size_t` variable can't be used, but the address of an `unsigned int` must be provided. Such situations are exceptional, though.

Other useful bit-represented types also exist. E.g., `uint32_t` is guaranteed to hold 32-bit unsigned values. Analogously, `int32_t` holds 32-bit signed values. Corresponding types exist for 8-, 16- and 64-bit values. These types are defined in the header file `cstdint`.

## 3.5 A new syntax for casts

Traditionally, C offers the following *cast* syntax:

```cpp
(typename)expression
```

Here `typename` is the name of a valid type, and `expression` is an expression.

C-style casts are now deprecated. Although C++ offers *function call* notation using the following syntax:

```cpp
typename(expression)
```

the function call notation does in fact not represent a cast, but a request to the compiler to construct an (anonymous) variable having type `typename` from `expression`. Although this form is very often used in C++, it should *not* be used for casting. Instead, there are now four *new-style casts* available, which are introduced in the following sections.

The C++11 standard defines the `shared_ptr` type (cf. section 18.4). To cast shared pointers, specialized casts should be used. These are discussed in section 18.4.5.

### 3.5.1 The `static_cast` operator

The cast converting conceptually comparable types to each other is:

```cpp
static_cast<type>(expression)
```

This type of cast is used to convert, e.g., a `double` to an `int`: both are numbers, but as the `int` has no fractions, precision is potentially reduced. But the converse also holds true. When the quotient of two `int` values must be assigned to a `double`, the fraction part of the division is lost unless a cast (of either the numerator or denominator to `double`) is used.

Here is an example of such a cast (assuming `quotient` is of type `double` and `lhs` and `rhs` are `int`-typed variables):

```cpp
quotient = static_cast<double>(lhs) / rhs;
```

If the cast is omitted, the division operator ignores the remainder as its operands are `int` expressions. Note that the division should be put outside of the cast expression. If the division is put inside (as in `static_cast<double>(lhs / rhs)`) an *integer division* has already been performed *before* the cast has had a chance to convert the type of an operand to `double`.

Another nice example of code in which it is a good idea to use the `static_cast<>()` operator is in situations where binary assignment operators are used in mixed-type expressions. Consider the following expression (assume `doubleVar` is a variable of type `double`):

```cpp
intVar += doubleVar;
```

This statement actually evaluates to:

```cpp
intVar = static_cast<int>(static_cast<double>(intVar) +
doubleVar);
```

Here `intVar` is first promoted to a `double`, and is then added as a `double` value to `doubleVar`. Next, the sum is cast back to an `int`. These two casts are a bit overdone. The same result is obtained by explicitly casting `doubleVar` to an `int`, thus obtaining an `int` value for the right-hand side of the expression:

```cpp
intVar += static_cast<int>(doubleVar);
```

A `static_cast` can also be used to undo or introduce the signed modifier of an `int`-typed variable. The C function `tolower` requires an `int` representing the value of an `unsigned char`. But `char` by default is a signed type. To call `tolower` using an available `char ch` we should use:

```cpp
tolower(static_cast<unsigned char>(ch))
```

Casts like these provide information to the compiler about how to handle the provided data. Very often (especially with data types differing only in size but not in representation) the cast won't require any additional code. Additional code is required, however, to convert one representation to another, e.g., when converting `double` to `int`.

### 3.5.2 The `const_cast` operator

The `const` keyword has been given a special place in casting. Normally anything `const` is `const` for a good reason. Nonetheless situations may be encountered where the `const` can be ignored. For these special situations the `const_cast` should be used. Its syntax is:

```cpp
const_cast<type>(expression)
```

A `const_cast<type>(expression)` expression is used to undo the `const` attribute of a (pointer) type.

The need for a `const_cast` may occur in combination with functions from the standard C library which traditionally weren't always as `const`-aware as they should. A function `strfun(char *s)` might be available, performing some operation on its `char *s` parameter without actually modifying the characters pointed to by `s`. Passing `char const hello[] = "hello";` to `strfun` produces the warning

```text
passing `const char *` as argument 1 of `fun(char *)` discards const
```

A `const_cast` is the appropriate way to prevent the warning:

```cpp
strfun(const_cast<char *>(hello));
```

### 3.5.3 The `reinterpret_cast` operator

The third new-style cast is used to change the *interpretation* of information: the `reinterpret_cast`. It is somewhat reminiscent of the `static_cast`, but `reinterpret_cast` should be used when it is *known* that the information as defined in fact is or can be interpreted as something completely different. Its syntax is:

```cpp
reinterpret_cast<pointer type>(pointer expression)
```

A `reinterpret_cast<type>(expression)` operator is appropriately used to reinterpret a `void *` to a pointer of a well-known type. Void pointers are encountered with functions from the C library like `qsort`. The `qsort` function expects a pointer to a comparison function having two `void const *` parameters. In fact, the `void const *`s point to data elements of the array to sort, and so the comparison function may cast the `void const *` parameters to pointers to the elements of the array to be sorted. E.g., if the array is an `int array[]` and the compare function's parameters are `void const *p1, void const *p2` then the compare function may obtain the address of the `int` pointed to by `p1` by using:

```cpp
reinterpret_cast<int const *>(p1)
```

Another example of a `reinterpret_cast` is found in combination with the `write` functions that are available for files and streams. In C++ streams are the preferred interface to, e.g., files. Output streams (like `cout`) offer `write` members having the prototype

```cpp
write(char const *buffer, int length)
```

To write a `double` to a stream using `write` a `reinterpret_cast` is needed as well. E.g., to write the raw bytes of a variable `double value` to `cout` we would use:

```cpp
cout.write(reinterpret_cast<char const *>(&value), sizeof(double));
```

All casts are potentially dangerous, but the `reinterpret_cast` is the most dangerous of all casts. Effectively we tell the compiler: back off, we know what we're doing, so stop fussing. All bets are off, and we'd better know what we're doing in situations like these. As a case in point consider the following code:

```cpp
int value = 0x12345678;      // assume a 32-bit int

cout << "Value's first byte has value: " << hex <<
        static_cast<int>(
            *reinterpret_cast<unsigned char *>(&value)
        );
```

The above code produces different results on little- and big-endian computers. Little-endian computers show the value 78, big-endian computers the value 12. Also note that the different representations used by little- and big-endian computers render the previous example (`cout.write(...)`) non-portable over computers of different architectures.

As a rule of thumb: if circumstances arise in which casts have to be used, clearly document the reasons for their use in your code, making double sure that the cast does not eventually cause a program to misbehave.

### 3.5.4 The `dynamic_cast` operator

Finally there is a new-style cast that is used in combination with polymorphism (see chapter 14). Its syntax is:

```cpp
dynamic_cast<type>(expression)
```

It is used at run-time to convert a pointer to an object of some class (e.g., `Base`) to a pointer to an object of another class (e.g., `Derived`) which is found further down its so-called *class hierarchy* (this is also called *downcasting*). At this point in the *Annotations* a `dynamic_cast` cannot yet be discussed extensively, but we return to this topic in section 14.6.1.
