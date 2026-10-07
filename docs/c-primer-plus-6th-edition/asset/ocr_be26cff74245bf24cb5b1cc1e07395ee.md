# Enumerations 151

By default, enumerators are assigned integer values starting with 0 for the first enumerator, 1 for the second enumerator, and so forth. You can override the default by explicitly assigning integer values. You'll see how later in this chapter.

You can use an enumeration name to declare a variable of the enumeration type: spectrum band; // band a variable of type spectrum

An enumeration variable has special properties, which we'll examine now. The only valid values that you can assign to an enumeration variable without a type cast are the enumerator used in defining the type. Thus, we have the following:

```
band = blue; // valid, blue is an enumerator
band = 2000; // invalid, 2000 is not an enumerator
```

Thus, a spectrum variable is limited to just eight possible values. Some compilers issue a compiler error if you attempt to assign an invalid value, whereas others issue a warning. For maximum portability, you should regard assigning a non-enum value to an enum as an error.

Only the assignment operator is defined for enumerations. In particular, arithmetic operations are not defined:

```
band = orange; // valid
++++; // not valid, defined in Chapter 5
band = orange + red; // not valid, a little tricky
```

However, some implementations do not honor this restriction. That can make it possible to violate the type limits. For example, if band has the value ultraviolet, or 7, then ++++; if valid, increments band to 8, which is not a valid value for a spectrum type. Again, for maximum portability, you should adopt the stricter limitations.

Enumerators are of integer type and can be promoted to type int, but int types are not converted automatically to the enumeration type:

```
int color = blue; // valid, spectrum type promoted to int
band = 3; // invalid, int not converted to spectrum
color = 3 + red; // valid, red converted to int
...
```

Note that in this example, even 3 corresponds to the enumerator green, assigning 3 to a band is a type error. But assigning green to band is fine because both type are spectrum. Again, some implementations do not enforce this restriction. In the expression 3 + red, addition is not defined for enumerators. However, red is converted to type int, and the result is type int. Because of conversion from enumeration to int in this situation, you can use enumerations in arithmetic expressions to combine them though arithmetic isn't defined for enumerations themselves.

```
band = orange + red; // not valid, a little tricky
```