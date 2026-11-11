In Java, the `char` type describes a *code unit* in the UTF-16 encoding.

I strongly recommend against using the `char` type in your programs unless you are actually manipulating UTF-16 code units. You are almost always better off treating strings as abstract data types—see Section 3.6, “Strings,” on p. 61.

# 3.3.5 The **boolean** Type

The `boolean` type has two values, `false` and `true`. It is used for evaluating logical conditions. You cannot convert between integers and `boolean` values.

![](bbox=[0.128, 0.376, 0.178, 0.415])

# C++ NOTE:

In C++, numbers and even pointers can be used in place of boolean values. The value 0 is equivalent to the bool value false, and a nonzero value is equivalent to true. This is *not* the case in Java. Thus, Java programmers are shielded from accidents such as

```
```cpp
if (x = 0) // oops... meant x == 0
```
```

In C++, this test compiles and runs, always evaluating to false. In Java, the test does not compile because the integer expression `x = 0` cannot be converted to a boolean value.

# 3.4 Variables and Constants

As in every programming language, variables are used to store values. Constants are variables whose values don’t change. In the following sections, you will learn how to declare variables and constants.

# 3.4.1 Declaring Variables