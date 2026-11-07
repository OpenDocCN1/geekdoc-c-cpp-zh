The syntax for enumeration type is:

```
```cpp
enum typeName {value1, value2, ...};
```
```

in which value1, value2, . . . are identifiers called **enumerators**. In C++, **enum** is a reserved word.

By listing all of the values between the braces, you also specify an ordering between the values. That is, value1 < value2 < value3 < . . . . Thus, the enumeration type is an ordered set of values. Moreover, the default value assigned to these enumerators starts at 0. That is, the default value assigned to value1 is 0, the default value assigned to value2 is 1, and so on. (You can assign different values—other than the default values—for the enumerators when you define the enumeration type.) Also notice that the enumerators value1, value2, . . . are *not* variables.

# EXAMPLE 8-1

The statement:

```
```cpp
enum colors {BROWN, BLUE, RED, GREEN, YELLOW};
```
```

defines a new data type called colors, and the values belonging to this data type are BROWN, BLUE, RED, GREEN, and YELLOW.

# EXAMPLE 8-2

The statement:

```
```cpp
enum standing {FRESHMAN, SOPHOMORE, JUNIOR, SENIOR};
```
```

defines standings to be an enumeration type. The values belonging to standing are FRESHMAN, SOPHOMORE, JUNIOR, and SENIOR.

# EXAMPLE 8-3

Consider the following statements:

```
```cpp
enum grades {'A', 'B', 'C', 'D', 'F'}; //illegal enumeration type
enum places {1ST, 2ND, 3RD, 4TH};   //illegal enumeration type
```
```