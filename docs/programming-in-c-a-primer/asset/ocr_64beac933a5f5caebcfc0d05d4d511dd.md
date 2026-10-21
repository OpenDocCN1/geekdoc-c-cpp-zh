# 15

# Operator Overloading

# 15.1 Introduction

Operator overloading is one of the many exciting features of object-oriented programming. C# supports the idea of operator overloading. It means that C# operators can be defined to work with the user-defined data types such as structs and classes in much the same way as the built-in types. For instance, C# permits us to add two class objects with the same syntax that is applied to the basic types.

Example:

```
Vector u1, u2, u3;
...                 //Initialize u1 and u2 here

u3 = u1 + u2;       //adding two objects, u1 and u2
```

where Vector is a class or a struct. Two vectors u1 and u2 are added (like a simple type) to give a third vector (u3). This means, C# has the ability to provide the operators with a special meaning for a data type. This mechanism of giving such special meaning to an operator is known as operator overloading.

Operator overloading provides a flexible option for the creation of new definitions for most of the C# operators. We can almost create a new language of our own by the creative use of the method and operator overloading techniques.

# 15.2 OVERLOADABLE OPERATORS

There are quite a number of operators in C# that can be overloaded. There are also many others that cannot be overloaded. They are listed in Tables 15.1 and 15.2.

# Table 15.1 Overloadable operators

| CATEGORY | OPERATORS |
|---|---|
| Binary arithmetic | +, *, /, -, % |
| Unary arithmetic | +, -, ++, -- |
| Binary bitwise | &, |, ^, <<, >> |
| Unary bitwise | !, ~, true, false |
| Logical operators | ==, !=, >, >=, <, <=, > |