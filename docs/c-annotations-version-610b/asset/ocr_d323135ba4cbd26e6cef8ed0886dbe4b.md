+   - `p`, to specify the power in hexadecimal floating point numbers. E.g. `0x10p4`. The exponent itself is read as a decimal constant and can therefore not start with `0x`. The exponent part is interpreted as a power of 2. So `0x10p2` is (decimal) equal to 64: 16 * 2^2.
+   - `U` can be used as postfix to an integral value to indicate an unsigned value, rather than an `int`. It may also be combined with the postfix `L` to produce an unsigned long int value.

And, of course: the `x` and `a` until `f` characters can be used to specify hexadecimal constants (optionally using capital letters).

# ### 3.4.1 The data type `bool`

The type `bool` represents boolean (logical) values, for which the (now reserved) constants `true` and `false` may be used. Except for these reserved values, integral values may also be assigned to variables of type `bool`, which are then implicitly converted to `true` and `false` according to the following conversion rules (assume `intValue` is an `int`-variable, and `boolValue` is a `bool`-variable):

```
```cpp
// from int to bool:
boolValue = intValue ? true : false;

// from bool to int:
intValue = boolValue ? 1 : 0;
```
```

Furthermore, when `bool` values are inserted into streams then `true` is represented by 1, and `false` is represented by 0. Consider the following example:

```
```cpp
cout << "A true value: " << true << "\n"
     "A false value: " << false << '\n';
```
```

The `bool` data type is found in other programming languages as well. **Pascal** has its type `Boolean`; **Java** has a `boolean` type. Different from these languages, C++'s type `bool` acts like a kind of `int` type. It is primarily a documentation-improving type, having just two values `true` and `false`. Actually, these values can be interpreted as `enum` values for 1 and 0. Doing so would ignore the philosophy behind the `bool` data type, but nevertheless: assigning `true` to an `int` variable neither produces warnings nor errors.

Using the `bool`-type is usually clearer than using `int`. Consider the following prototypes:

```
```cpp
bool exists(char const *fileName);   // (1)
int  exists(char const *fileName);   // (2)
```
```

With the first prototype, readers expect the function to return `true` if the given filename is the name of an existing file. However, with the second prototype some ambiguity arises: intuitively the return value 1 is appealing, as it allows constructions like

```
```cpp
if (exists("myfile"))
    cout << "myfile exists";
```
```

On the other hand, many system functions (like `access`, `stat`, and many other) return 0 to indicate a successful operation, reserving other values to indicate various types of errors.

As a rule of thumb I suggest the following: if a function should inform its caller about the success or failure of its task, let the function return a `bool` value. If the function should return success or various types of errors, let the function return `enum` values, documenting the situation by its various symbolic constants. Only when the function returns a conceptually meaningful integral value (like the sum of two `int` values), let the function return an `int` value.