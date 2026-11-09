|  |  |  |  |  |
|---|---|---|---|---|
| Short | 16-bit integer type | signed | 0 | -32,768 to 32,767 |
| Long | 64-bit integer type | signed | 0L | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |

# 2. Reference Type

The reference data type stores the reference to a variable instead of storing the actual data. By using multiple variables, reference types can point to a memory location and in case the memory location is changed by one of the variables, the other variable will automatically change its value.

# 3. Object type

Object data type is considered as the base class for all data types that are used in C#. Moreover, object types can also be assigned values of other types, reference types, user defined types, and value types as well.

# 4. Pointer data type

Pointer data type contains memory address of the variable value and has the syntax as follows:

```
Type* identifier;
```

# Operators

C# makes use of operators in the same way as the other major programming languages such as C and C++. The set of built-in operators include Arithmetic operators, Relational operators, Bitwise operators, Logical operators, Misc operators, and Assignment operators.

# Functions and Methods

In C# programming language, a function allows the programmers to encapsulate a specific part of the code and utilize it from other sections of the code as well. As it stops the need to rewrite the code, we can access a function from multiple places and perform the required operations as well. The functions in C# are declared by using the following syntax:

```
<visibility> <return type> <name>(<parameters>)
```