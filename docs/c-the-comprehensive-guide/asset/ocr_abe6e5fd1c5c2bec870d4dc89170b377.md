This is quite a tricky expression:

+   - `(result = read(buffer, 100)) != 0` calls the function `read()`.
+   - Its result is assigned to `result`.
+   - The result of this expression is then compared to 0. With `!= 0`, it checks if it is not equal to 0.
+   - And this is true or false, so the `if` can decide which way to go.

However, use such assignments within other expressions sparingly. Under no circumstances should you perform “magic” and change values in the middle of a calculation:

```
3 + ((number = 2) * 4) -- 6 * (value = (6/2)) // ⚡ not good style at all
```

No one will be able to understand that anymore. It is downright wrong also to use the target of the assignment elsewhere in the expression:

```
3 + (number = 2) * (number = 4) + 6          // ⚡ modified and used
```

This is faulty code of the sort that allows the program to do whatever it wants—not what you want (*undefined behavior*).

> **Using an Assignment as Part of a Larger Expression Is Dangerous!**
> 
> Do not reuse the target of an assignment in the same statement. The result is undefined: the compiler does not have to warn you. This applies to all operations with side effects that modify a variable.

# 9.8  Type Casting

It is easy to explain type conversion for the previously introduced int, bool, double, and string and their relatives because there is not much to convert with these types yet. Later, however, this will become an extensive topic that I will return to multiple times. In the context of expressions, I will exemplify the conversion between int and bool to illustrate the concept.

You can convert an int to a bool by simply using the type name as a function:

```
int value = 10;
bool yesNo = bool(value);  // function notation for type conversion
```

Coming from C, there is another notation for this. It is still very popular, and you will see it often:

```
bool yesNo = (bool)value;  // C notation for type conversion
```