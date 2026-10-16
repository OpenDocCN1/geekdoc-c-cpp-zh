abstractly, we can consider the type name to be essentially identical to the set of values it represents, and we can state the following:

DEFINITION:1. A data type is a set of values.

Thus, the declaration of x as an int says that the value of x must be in the set of integers as defined by the language (and the implementation), or, in mathematical terminology (using ∈ for membership) the declaration

```
int x;
```

means the same as:

value of x ∈ Integers

where Integers is the set of integers as defined by the language and implementation. In Java, for example, this set is always the set of integers from to 22,147,483,648 to 2,147,483,647, since integers are always stored in 32-bit two’s-complement form.

A data type as a set can be specified in many ways: It can be explicitly listed or enumerated, it can be given as a subrange of otherwise known values, or it can be borrowed from mathematics, in which case the finiteness of the set in an actual implementation may be left vague or ignored.⁵ Set operations can also be applied to get new sets out of old (see below).

A set of values generally also has a group of operations that can be applied to the values. These operations are often not mentioned explicitly with the type, but are part of its definition. Examples include the arithmetic operations on integers or reals, the subscript operation [ ] on arrays, and the member selector operator on structure or record types. These operations also have specific properties that may or may not be explicitly stated [e.g., (x + 1) − 1 = x or x + y = y + x]. Thus, to be even more precise, we revise our first definition to include explicitly the operations, as in the following definition:

DEFINITION:2. A data type is a set of values, together with a set of operations on those values having certain properties.

In this sense, a data type is actually a mathematical algebra, but we will not pursue this view to any great extent here. (For a brief look at algebras, see the mathematics of abstract data types in Chapter 11.)

As we have already noted, a language translator can make use of the set of algebraic properties in a number of ways to assure that data and operations are used correctly in a program. For example, given a statement such as

```
z = x / y;
```

a translator can determine whether x and y have the same (or related) types, and if that type has a division operator defined for its values (thus also specifying which division operator is meant, resolving any

⁵In C, these limits are defined in the standard header files limits.h and float.h. In Java, the classes associated with each of the basic data types record these limits (for example, java.lang.Integer.MAX_VALUE 5 2147483647).