# Automatic Storage Class

Automatic storage class assigns a variable to its default storage type. auto keyword is used to declare automatic variables. However, if a variable is declared without any keyword inside a function, it is automatic by default. This variable is visible only within the function it is declared and its lifetime is same as the lifetime of the function as well. Once the execution of function is finished, the variable is destroyed.

# Syntax of Automatic Storage Class Declaration:

```
datatype var_name [= value];
or
auto datatype var_name [= value];
```

# Example of Automatic Storage Class:

```
auto int x;
float y = 5.67;
```

# External Storage Class

External storage class assigns a reference to a global variable declared outside the given program. extern keyword is used to declare external variables. They are visible throughout the program and its lifetime is same as the lifetime of the program where it is declared. This visible to all the functions present in the program.

# Syntax of External Storage Class Declaration:

```
extern datatype var_name;
```

Example:

```
extern float var1;
```

Examples of External Storage Class

Example 1: C++ program to create and use external storage.

```
File: sub.cpp
int test=100;   // assigning value to test
void multiply(int n)
{}
```