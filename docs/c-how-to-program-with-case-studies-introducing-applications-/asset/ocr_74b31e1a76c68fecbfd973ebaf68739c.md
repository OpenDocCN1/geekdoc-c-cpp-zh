# Self Check

1 (Fill-In) The structure member operator ________ and the structure pointer operator ________ can be used to access structure members.

Answer: . (dot), ->.

2 (True/False) The expression cardPtr->suit is equivalent to (*cardPtr).suit, which dereferences the pointer and accesses the member suit using the structure member operator. The parentheses are optional.

Answer: False. The expressions, as shown, are equivalent. The parentheses are needed here because the structure member operator (.) has higher precedence than the pointer dereferencing operator (*).

# 10.5 Using Structures with Functions

With structures, you can pass to functions:

+   - individual structure members,
+   - entire structure objects, or
+   - pointers to structure objects.

Individual structure members and entire structure objects are passed by value, so functions cannot modify them in the caller. To pass a structure by reference, use the structure object's address. Passing structures by reference is more efficient than passing structures by value, which requires the entire structure to be copied. Arrays of structure objects—like all other arrays—are automatically passed by reference.

PERF

# Passing an Array By Value

In Chapter 6, we stated that you can use a structure to pass an array by value. To do so, create a structure with an array member. Structures are passed by value, so its members are passed by value.

# Self Check

1 (Fill-In) Structure objects and individual structure members are passed to functions by ________.

Answer: value.

# 10.6 typedef

The keyword typedef enables you to create synonyms (or aliases) for previously defined types. It's commonly used to create shorter names for struct types and simplify declarations of types like function pointers. For example, the following typedef defines Card as a synonym for type struct card:

```
typedef struct card Card;
```