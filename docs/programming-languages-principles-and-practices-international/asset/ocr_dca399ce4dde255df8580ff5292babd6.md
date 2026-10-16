# ## 7.1 Attributes, Binding, and Semantic Functions

A fundamental abstraction mechanism in any programming language is the use of **names, or identifiers,** to denote language entities or constructs. In most languages, variables, procedures, and constants can have names assigned by the programmer. A fundamental step in describing the semantics of a language is to describe the conventions that determine the meaning of each name used in a program.

In addition to names, a description of the semantics of most programming languages includes the concepts of **location** and **value**. Values are any storable quantities, such as the integers, the reals, or even array values consisting of a sequence of the values stored at each index of the array. Locations are places values can be stored. Locations are like addresses in the memory of a specific computer, but we can think of them more abstractly than that. To simplify, we can think of locations as being numbered by integers starting at 0 and going up to some maximum location number.

The meaning of a name is determined by the properties, or **attributes,** associated with the name. For example, the C declaration¹

```
```c
const int n = 5;
```
```

makes n into an integer constant with value 5. That is, it associates to the name n the data type attribute “integer constant” and the value attribute 5. (In C, the constant attribute—that n can never change its value—is part of the data type; in other languages this may be different.) The C declaration

```
```c
int x;
```
```

associates the attribute “variable” and the data type “integer” to the name x. The C declaration

```
```c
double f(int n){
...
}
```
```

associates the attribute “function” and the following additional attributes to the name f:

+   1. The number, names, and data types of its parameters (in this case, one parameter with name n and data type “integer”)
+   2. The data type of its returned value (in this case, “double”)
+   3. The body of code to be executed when f is called (in this case, we have not written this code but just indicated it with three dots)

Declarations are not the only language constructs that can associate attributes to names. For example, the assignment:

```
```c
x = 2;
```
```

associates the new attribute “value 2” to the variable x. And, if y is a pointer variable² declared as:

```
```cpp
int* y;
```
```

the C++ statement

```
```cpp
y = new int;
```
```