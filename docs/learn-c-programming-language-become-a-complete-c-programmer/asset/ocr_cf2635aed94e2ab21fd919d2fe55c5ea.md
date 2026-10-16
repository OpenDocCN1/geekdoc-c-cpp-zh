A value of integral type may be explicitly converted to an enumeration type. The result of such a conversion is undefined unless the value is within the range of the enumeration’s underlying type. For example:

```
enum class Flag : char{ x=1, y=2, z=4, e=8 };
Flag f0 {}; // f0 gets the default value 0
Flag f1 = 5; // type error: 5 is not of type Flag
Flag f2 = Flag{5}; // error: no narrowing conversion to an enum class Flag
Flag f3 = static_cast<Flag>(5); // bruteforce
Flag f4 = static_cast<Flag>(999); // error: 999 is not a char value (maybe not caught)
```

The last assignments show why there is no implicit conversion from an integer to an enumeration; most integer values do not have a representation in a particular enumeration. Each enumerator has an integer value. We can extract that value explicitly. For example:

```
int i = static_cast<int>(Flag::y); // becomes 2
char c = static_cast<char>(Flag::e); // becomes 8
```

The notion of a range of values for an enumeration differs from the enumeration notion in the Pascal family of languages. However, bit-manipulation examples that require values outside the set of enumerators to be well defined (e.g., the Printer_flags example) have a long history in C and C++.

The sizeof an enum class is the sizeof of its underlying type. In particular, if the underlying type is not explicitly specified, the size is sizeof(int).

# 8.4.2 Plain enums

A “plain enum” is roughly what C++ offered before the enum classes were introduced, so you’ll find them in lots of C and C++98-style code. The enumerators of a plain enum are exported into the enum’s scope, and they implicitly convert to values of some integer type. Consider the examples from §8.4.1 with the “class” removed:

```
enum Traffic_light { red, yellow, green };
enum Warning { green, yellow, orange e, red }; // fire alert levels
// error: two definitions of yellow (to the same value) // error: two definitions of red (to different values)

Warning a1 = 7;
int a2 = green;
int a3 = Warning::green; Warning a4 = Warning::green;

// error: no int->Warning conversion // OK: green is in scope and converts to int // OK: Warning->int conversion
// OK

void f(Traffic_light x) {
    if (x == 9) { /* ... */ } if (x == red) { /* ... */ }

    // OK (but Traffic_light doesn’t have a 9) // error: two reds in scope
    if (x == Warning::red) { /* ... */ } // OK (Ouch!)
    if (x == Traffic_light::red) { /* ... */ } // OK
}
```