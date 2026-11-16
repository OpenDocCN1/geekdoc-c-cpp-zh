```
Shade color = Shade::Light;
Weight mass = Weight::Light;
```

In this case Shade and Weight are the scoped enumeration types defined above. Prefixing the type name to the value with the :: operator enables the compiler to distinguish between the two different values. Scoped enumerations require the type name prefix even if the program contains no other enumerated types. In modern C++ development, scoped enumerations are preferable to unscoped enumerations. You should be familiar with unscoped enumerations, though, as a lot of published C++ code and older C++ books use unscoped enumerations.

Whether scoped or unscoped, the value names within an enum type must be unique. The convention in C++ is to capitalize the first letter of an enum type and its associated values, although the language does not enforce this convention.

An enum type is handy for representing a small number of discrete, non-numeric options. For example, consider a program that controls the movements made by a small robot. The allowed orientations are forward, backward, left, right, up, and down. The program could encode these movements as integers, where 0 means left, 1 means backward, etc. While that implementation will work, it is not ideal. Integers may assume many more values than just the six values expected. The compiler cannot ensure that an integer variable representing a robot move will stay in the range 0..5. What if the programmer makes a mistake and under certain rare circumstances assigns a value outside of the range 0...5? The program then will contain an error that may result in erratic behavior by the robot. With enum types, if the programmer uses only the named values of the enum type, the compiler will ensure that such a mistake cannot happen.

A particular enumerated type necessarily has far fewer values than a type such as int. Imagine making an integer enum type and having to list all of its values! (The standard 32-bit int type represents over four billion values.) Enumerated types, therefore, are practical only for types that have a relatively small range of values.

# 3.10 Type Inference with auto

C++ requires that a variable be declared before it is used. Ordinarily this means specifying the variable's type, as in

```
int count;
char ch;
double limit;
```

A variable may be initialized when it is declared:

```
int count = 0;
char ch = 'Z';
double limit = 100.0;
```

Each of the values has a type: 0 is an int, 'Z' is a char, and 0.0 is a double. The auto keyword allows the compiler to automatically deduce the type of a variable if it is initialized when it is declared:

```
auto count = 0;
auto ch = 'Z';
auto limit = 100.0;
```

The auto keyword may not be used without an accompanying initialization; for example, the following declaration is illegal: