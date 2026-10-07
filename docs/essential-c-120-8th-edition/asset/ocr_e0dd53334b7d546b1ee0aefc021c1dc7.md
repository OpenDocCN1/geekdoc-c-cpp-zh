# Programming with null 175

Of course, having multiple ways to check whether a value is null raises the question as to which one to use. C# 7.0's enhanced is null and C# 9.0's is not null syntax are preferable if you are using a modern version of C#.

Obviously, if you are programming with C# 6.0 or earlier, the equality/inequality operators are the only option aside from object to check for null. The latter has a slight advantage since it is not possible to change the definition of the is expression and (albeit unlikely) introduce a minor performance hit. This renders is {} effectively obsolete. Using ReferenceEquals() is rare, but it does allow comparison of values that are of unknown data types, which is helpful when implementing a custom version of the equality operator (“Operator Overloading” (https://essentialsharp.com/operator-overloading) in Chapter 10).

Several of the rows in Table 4.4 leverage pattern matching, a concept covered in more detail in the “Pattern Matching” (https://essentialsharp.com/pattern-matching) section of Chapter 7.

# Null-Coalescing and Null-Coalescing Assignment Operators ??, ?=

The null-coalescing operator is a concise way to express “If this value is null, then use this other value.” It has the following form:

```
expression1 ?? expression2
```

The null-coalescing operator also uses a form of short-circuiting. If expression1 is not null, the value is the result of the operator and the other expression is not evaluated. If expression1 evaluates to null, the value of expression2 is the result of the operator. Unlike the conditional operator, the null-coalescing operator is a binary operator.

Listing 4.37 illustrates the use of the null-coalescing operator.

# LISTING 4.37: Null-Coalescing Operator

```
string? fullName = GetFileNamePath();
...
// Null-coalescing operator
string fileName = GetFileName() ?? "config.json";
```