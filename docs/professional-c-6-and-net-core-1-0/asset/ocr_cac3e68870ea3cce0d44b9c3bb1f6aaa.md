> NOTE Later in this chapter in the “Implementing Custom Index Operators” section, you can read how to create index operators in your own classes.

# Nullable Types and Operators

An important difference between value types and reference types is that reference types can be null. A value type, such as int, cannot be null. This is a special issue on mapping C# types to database types. A database number can be null. In earlier C# versions, a solution was to use a reference type for mapping a nullable database number. However, this method affects performance because the garbage collector needs to deal with reference types. Now you can use a nullable int instead of a normal int. The overhead for this is just an additional Boolean that is used to check or set the null value. A nullable type still is a value type.

With the following code snippet, the variable i1 is an int that gets 1 assigned to it. i2 is a nullable int that has i1 assigned. The nullability is defined by using the ? with the type. int? can have an integer value assigned similar to the assignment of i1. The variable i3 demonstrates that assigning null is also possible with nullable types.

```
int i1 = 1;
int? i2 = 2;
int? i3 = null;
```

Every struct can be defined as a nullable type as shown with long? and DateTime?:

```
long? l1 = null;
DateTime? d1 = null;
```

If you use nullable types in your programs, you must always consider the effect a null value can have when used in conjunction with the various operators. Usually, when using a unary or binary operator with nullable types, the result will be null if one or both of the operands is null. For example:

```
int? a = null;

int? b = a + 4;      // b = null
int? c = a * 5;      // c = null
```

When comparing nullable types, if only one of the operands is null, the comparison always equates to false. This means that you cannot assume a condition is true just because its opposite is false, as often happens in programs using non-nullable types. For example, in the following example if a is null, the else clause is always invoked no matter whether b has a value of +5 or -5.

```
int? a = null;
int? b = -5;
```