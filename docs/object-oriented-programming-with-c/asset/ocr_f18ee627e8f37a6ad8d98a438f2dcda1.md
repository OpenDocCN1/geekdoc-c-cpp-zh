```
```cpp
char ch = static_cast<char>(m);
```
```

The first statement casts the variable **m** to type **double** and the second casts it to type **char**.

Why use this new type when the old style still works? The syntax of the old one blends into the rest of the lines and therefore it is difficult to locate them. The new format is easy to spot and to search for using automated tools.

# The const_cast Operator

The **const_cast** operator is used to explicitly override **const** or **volatile** in a cast. It takes the form

```
```cpp
const_cast<type>(object)
```
```

Since the purpose of this operator is to change its **const** or **volatile** attributes, the *target type* must be the same as the *source type*. It is mostly used for removing the const_ness of an object.

# The reinterpret_cast Operator

The **reinterpret_cast** is used to change one type into a fundamentally different type. For example, it can be used to change a pointer type object to integer type object or vice versa. It takes the following form:

```
```cpp
reinterpret_cast<type>(object)
```
```

This operator should be used for casting inherently incompatible types. Examples:

```
```cpp
int m;
float x;
```
```