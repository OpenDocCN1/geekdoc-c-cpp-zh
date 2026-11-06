```
```cpp
        // process myString
}
```
```

The above example requires additional clarification. Often a variable can profitably be given local scope, but an extra check is required immediately following its initialization. The initialization and the test cannot both be combined in one expression. Instead two nested statements are required. Consequently, the following example won’t compile either:

```
```cpp
if ((int c = getchar()) && strchr("aeiou", c)
    printf("Saw a vowel\\n");
```
```

If such a situation occurs, either use two nested if statements, or localize the definition of int c using a nested compound statement:

```
```cpp
if (int c = getchar())                 // nested if-statements
    if (strchr("aeiou", c))
        printf("Saw a vowel\\n");

{
    int c = getchar();                  // nested compound statement
    if (c && strchr("aeiou", c))
        printf("Saw a vowel\\n");
}
```
```

# 2.5.12  The keyword ‘typedef’

The keyword `typedef` is still used in C++, but is not required anymore when defining `union`, `struct` or `enum` definitions. This is illustrated in the following example:

```
```cpp
struct SomeStruct
{
    int       a;
    double    d;
    char      string[80];
};
```
```

When a `struct`, `union` or other compound type is defined, the tag of this type can be used as type name (this is SomeStruct in the above example):

```
```cpp
SomeStruct what;

what.d = 3.1415;
```
```

# 2.5.13  Functions as part of a struct

In C++ we may define functions as members of structs. Here we encounter the first concrete example of an object: as previously described (see section 2.4), an object is a structure containing data while specialized functions exist to manipulate those data.

A definition of a `struct Point` is provided by the code fragment below. In this structure, two `int` data fields and one function draw are declared.

```
```cpp
struct Point              // definition of a screen-dot
{
```
```