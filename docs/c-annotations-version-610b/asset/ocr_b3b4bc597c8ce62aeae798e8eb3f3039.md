# 3.3. MORE EXTENSIONS TO C

```
OK        = 10,
MAYBE_OK   // 11, by implication
};
```

Enum classes use int values by default, but the used value type can easily be changed using the : type notation, as in:

```
enum class CharEnum: unsigned char
{
    NOT_OK,
    OK
};
```

To use a value defined in an enum class its enumeration name must be provided as well. E.g., OK is not defined, CharEnum::OK is.

Using the data type specification (noting that it defaults to int) it is possible to use enum class forward declarations. E.g.,

```
enum Enum1;                 // Illegal: no size available
enum Enum2: unsigned int;  // Legal in C++11: explicitly declared type

enum class Enum3;          // Legal in C++11: default int type is used
enum class Enum4: char;    // Legal in C++11: explicitly declared type
```

# 3.3.4  Initializer lists (C++11)

The C language defines the initializer list as a list of values enclosed by curly braces, possibly themselves containing initializer lists. In C these initializer lists are commonly used to initialize arrays and structs.

C++ extends this concept in the C++11 standard by introducing the type initializer_list<Type> where Type is replaced by the type name of the values used in the initializer list. Initializer lists in C++ are, like their counterparts in C, recursive, so they can also be used with multi-dimensional arrays, structs and classes.

Like in C, initializer lists consist of a list of values surrounded by curly braces. But unlike C, functions can define initializer list parameters. E.g.,

```
void values(std::initializer_list<int> iniValues)
{
}
```

A function like values could be called as follows:

```
values({2, 3, 5, 7, 11, 13});
```

The initializer list appears as an argument which is a list of values surrounded by curly braces. Due to the recursive nature of initializer lists a two-dimensional series of values can also be passes, as shown in the next example:

```
void values2(std::initializer_list<int> iniValues)
{
}
```

```
values2({{1, 2}, {2, 3}, {3, 5}, {4, 7}, {5, 11}, {6, 13}});
```