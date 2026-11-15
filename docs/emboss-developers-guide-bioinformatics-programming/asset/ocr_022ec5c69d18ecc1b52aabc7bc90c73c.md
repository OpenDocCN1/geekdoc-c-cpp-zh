guaranteed to be of a minimum size and no larger than the following type. For example, an int is never longer than a long int. Similarly, the header float.h (or equivalent) defines constants such that a floating type is always at least as precise as the previous type. For example, a double is always at least as precise as a float.

In addition to the fundamental types described above, C defines the void type which specifies an empty value and is used, for example, for the return type of functions that do not return a value.

There are also enumerations, unique types that are associated with a set of named constant integer values.

# 5.1.2 Fundamental AJAX datatypes

# 5.1.2.1 Integer types

The exact size and precision of the fundamental C datatypes (excluding char) is implementation-dependent. To avoid any potential problems with these system-dependent limits, AJAX defines in the AJAX file ajarch.h a new set of fundamental datatypes as follows:

| Type | Description |
|---|---|
| ajshort | Short integer |
| ajint | Standard integer |
| ajlong | Long integer |
| ajushort | Unsigned short integer |
| ajuint | Unsigned standard integer |
| ajulong | Unsigned long integer |

There are some differences between the systems listed in ajarch.h but the typical definitions are as follows:

```
typedef short ajshort;
typedef int ajint;
typedef long long ajlong;
typedef unsigned int ajuint;
typedef unsigned short ajushort;
typedef unsigned long long ajulong;
```

An ajint is typically 32 bits and an ajlong typically 64 bits. Use ajint, if 32 bits is enough, instead of int. Use ajlong instead of long or long long. That said, standard C int and long should be used in some circumstances, for example as parameters to C system library functions.

You should match your datatype to what you need. If, for example, you are using an Alpha box then both your int and long variables will be 64 bits. In this case don't use only ajlong out of laziness as your code may run more slowly on other platforms.