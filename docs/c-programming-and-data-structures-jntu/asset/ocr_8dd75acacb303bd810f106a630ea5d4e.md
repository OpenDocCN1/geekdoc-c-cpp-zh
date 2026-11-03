regarding a student. Each student will have a name, roll number and branch of study. This entire information cannot be stored in a single array as student information consists of data of different types [name is a string, roll number is an integer and branch is a string]. To handle such string of data, C provides a derived data type known as structure.

![](bbox=[0.3, 0.25, 0.7, 0.4])

# Structure definition :

A structure is a collection of data items of different datatypes under a single name. Or, a structure is a collection of heterogeneous data items.

A structure is declared as follows

```
Struct < tag >
{
    Data type member1;
    Data type member2;
    .........
    ..........
    Data type member n;
};
```

+   * In this declaration struct is a keyword.
+   * <tag> is the name given to the structure declared.
+   * Data type can be integer, float, char or any other data types.
+   * member1, member2,......member n are members of structures. Individual members can be variable, pointers, arrays or other structures.
+   * Individual members cannot be initialized within structure definition. After structure has been declared, individual structure type variable are declared as follows.
+   Struct <tag> variable1,variable2........variable n;
+   * Variable 1, variable2..........variable n are structure variables of type tag.
+   * After closing bracket semicolon ';' must be specified.
+   * Members of structure themselves do not occupy any space. Memory is allocated only after declaring structure variables.

Structure can be declared as,

```
Struct tag
{
    Type 1 data 1;
    Type 2 data 2;
```