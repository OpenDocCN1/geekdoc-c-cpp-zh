there is no way you can make such an assignment as

```
objects[3] = 3;
```

and no opportunity to put the wrong type of thing into strings through objects, because
objects doesn't have any method that takes an element in. So, here the assignment hypothetically
could work without issues:

```
IEnumerable<object> objects = strings;
```

If you can enumerate through strings of System.Object and use the elements in the enumeration
s some operations over System.Object, those operations should work even if you enumerate
instances of System.String. Why? Because.String is assignable to a System.Object, so you
pass a System.String parameter to an operation (method) expecting System.Object.

The surprising fact is that this code works in C# 4.0, although it does not compile with C# 3.0.

# # Bird's View of Variance

The concept of how types can be substituted with other is called variance. Many forms of
variance have been working in C# since the first version. For example, method return values
can be substituted with derived types. Also, there are many forms that do not work.

Understanding the basics of variance will help you in becoming a more productive developer. The
section provides a brief overview of this topic from a (more theoretic) view without
t intent of completeness.

Variance is an attribute of an operation related to a type in the type system of a programming
language. The "operation" in this context can be a type conversion, some on the rule, or any
operation that carries out transformations. In the type system, you can compare types X and Y,
and the result of this comparison is one and only one of the following:

+   - X and Y are equal.
- X is greater than Y.
- X is less than Y.
- X is not related to Y.

According to this comparison, you can define ordering (from the lowest to the highest) among the
types, they are related to each other. You say an operation over the types in the type
system is one of the following:

+   - Covariant — This is if it preserves the ordering of types, or their unrelatedness;
- Contravariant — This is if it reverses the ordering of types, and keeps their equality and
unrelatedness;
- Invariant — This is if it is not of this nature.

One of the key factors that influences how variance is interpreted for a concrete type system of
programming language is the type comparator operator between X and Y.