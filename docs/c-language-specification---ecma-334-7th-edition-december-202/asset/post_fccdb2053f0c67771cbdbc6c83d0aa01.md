
- if e has integral type or enum type, or a nullable form of one of those, and v has integral type, the pattern P matches the value e if the result of the expression e == v is true; otherwise, the pattern P matches the value e if object.Equals(e, v) returns true.

Example: The switch statement in the following method uses five constant patterns in its case labels.

```
static decimal GetGroupTicketPrice(int visitorCount)
{
    switch (visitorCount)
    {
        case 1: return 12.0m;
        case 2: return 20.0m;
        case 3: return 27.0m;
        case 4: return 32.0m;
        case 0: return 0.0m;
        default: throw new ArgumentException(...);
    }
}
```

end example

### 11.2.4 Var pattern

A var_pattern matches every value. That is, a pattern-matching operation with a var_pattern always succeeds.

A var_pattern is applicable to every type.

```
var_pattern
    : 'var' designation
    ;
designation
    : simple_designation
    ;
```

Given a pattern input value (§11.1) e, if designation is the identifier _, it denotes a discard (§9.2.9.1), and the value of e is not bound to anything. (Although a declared variable with that name may be in scope at that point, that named variable is not seen in this context.) If designation is any other identifier, at runtime the value of e is bound to a newly introduced local variable (§9.2.9) of that name whose type is the static type of e, and the pattern input value is assigned to that local variable.

It is an error if the name var would bind to a type where a var_pattern is used.

### 11.3 Pattern subsumption

In a switch statement, it is an error if a case's pattern is subsumed by the preceding set of unguarded cases (§13.8.3). Informally, this means that any input value would have been matched by one of the previous cases. The following rules define when a set of patterns subsumes a given pattern.

A pattern P would match a constant k if the specification for that pattern's runtime behavior is that P matches k.

A set of patterns Q subsumes a pattern P if any of the following conditions hold:

- P is a constant pattern and any of the patterns in the set Q would match P's converted value
- P is a var pattern and the set of patterns Q is exhaustive (§11.4) for the type of the pattern input value (§11.1), and either the pattern input value is not of a nullable type or some pattern in Q would match null.
- P is a declaration pattern with type T and the set of patterns Q is exhaustive for the type T (§11.4).

### 11.4 Pattern exhaustiveness

Informally, a set of patterns is exhaustive for a type if some pattern in the set is applicable to every possible value of that type other than null. The following rules define when a set of patterns is exhaustive for a type:

A set of patterns Q is exhaustive for a type T if any of the following conditions hold:

- 1. T is an integral or enum type, or a nullable version of one of those, and for every possible value of T's non-nullable underlying type, some pattern in Q would match that value; or
- 2. Some pattern in Q is a var pattern; or
- 3. Some pattern in Q is a declaration pattern for type D, and there is an identity conversion, an implicit reference conversion, or a boxing conversion from T to D.

*Example:*

```
static void M(byte b)
{
    switch (b) {
        case 0: case 1: case 2: ... // handle every specific value of byte
            break;
        // error: the pattern 'byte other' is subsumed by the (exhaustive)
        // previous cases
        case byte other:
            break;
    }
}
```

*end example*

## 12. Expressions

### 12.1 General

An expression is a sequence of operators and operands. This clause defines the syntax, order of evaluation of operands and operators, and meaning of expressions.

### 12.2 Expression classifications

### 12.2.1 General

The result of an expression is classified as one of the following:

- A value. Every value has an associated type.
- A variable. Unless otherwise specified, a variable is explicitly typed and has an associated type, namely the declared type of the variable. An implicitly typed variable has no associated type.
- A null literal. An expression with this classification can be implicitly converted to a reference type or nullable value type.
- An anonymous function. An expression with this classification can be implicitly converted to a compatible delegate type or expression tree type.
- A tuple. Every tuple has a fixed number of elements, each with an expression and an optional tuple element name.
- A property access. Every property access has an associated type, namely the type of the property. Furthermore, a property access may have an associated instance expression. When an accessor of an instance property access is invoked, the result of evaluating the instance expression becomes the instance represented by `this` (§12.8.13).
- An indexer access. Every indexer access has an associated type, namely the element type of the indexer. Furthermore, an indexer access has an associated instance expression and an associated argument list. When an accessor of an indexer access is invoked, the result of evaluating the instance expression becomes the instance represented by `this` (§12.8.13), and the result of evaluating the argument list becomes the parameter list of the invocation.
- Nothing. This occurs when the expression is an invocation of a method with a return type of `void`. An expression classified as nothing is only valid in the context of a `statement_expression` (§13.7) or as the body of a `lambda_expression` (§12.19).

For expressions which occur as subexpressions of larger expressions, with the noted restrictions, the result can also be classified as one of the following:

- A namespace. An expression with this classification can only appear as the left-hand side of a `member_access` (§12.8.7). In any other context, an expression classified as a namespace causes a compile-time error.
- A type. An expression with this classification can only appear as the left-hand side of a member_access (§12.8.7). In any other context, an expression classified as a type causes a compile-time error.
- A method group, which is a set of overloaded methods resulting from a member lookup (§12.5). A method group may have an associated instance expression and an associated type argument list. When an instance method is invoked, the result of evaluating the instance expression becomes the instance represented by this (§12.8.13). A method group is permitted in an invocation_expression (§12.8.9) or a delegate_creation_expression (§12.8.16.6), and can be implicitly converted to a compatible delegate type (§10.8). In any other context, an expression classified as a method group causes a compile-time error.
- An event access. Every event access has an associated type, namely the type of the event. Furthermore, an event access may have an associated instance expression. An event access may appear as the left operand of the += and -= operators (§12.21.5). In any other context, an expression classified as an event access causes a compile-time error. When an accessor of an instance event access is invoked, the result of evaluating the instance expression becomes the instance represented by this (§12.8.13).
- A throw expression, which may be used in several contexts to throw an exception in an expression. A throw expression may be converted by an implicit conversion to any type.

A property access or indexer access is always reclassified as a value by performing an invocation of the get_accessor or the set_accessor. The particular accessor is determined by the context of the property or indexer access: If the access is the target of an assignment, the set_accessor is invoked to assign a new value (§12.21.2). Otherwise, the get_accessor is invoked to obtain the current value (§12.2.2).

An instance accessor is a property access on an instance, an event access on an instance, or an indexer access.

### 12.2.2 Values of expressions

Most of the constructs that involve an expression ultimately require the expression to denote a value. In such cases, if the actual expression denotes a namespace, a type, a method group, or nothing, a compile-time error occurs. However, if the expression denotes a property access, an indexer access, or a variable, the value of the property, indexer, or variable is implicitly substituted:

- The value of a variable is simply the value currently stored in the storage location identified by the variable. A variable shall be considered definitely assigned (§9.4) before its value can be obtained, or otherwise a compile-time error occurs.
- The value of a property access expression is obtained by invoking the get_accessor of the property. If the property has no get_accessor, a compile-time error occurs. Otherwise, a function member invocation (§12.6.6) is performed, and the result of the invocation becomes the value of the property access expression.
- The value of an indexer access expression is obtained by invoking the get_accessor of the indexer. If the indexer has no get_accessor, a compile-time error occurs. Otherwise, a function member invocation (§12.6.6) is performed with the argument list associated with the indexer access expression, and the result of the invocation becomes the value of the indexer access expression.
- The value of a tuple expression is obtained by applying an implicit tuple conversion (§10.2.13) to the type of the tuple expression. It is an error to obtain the value of a tuple expression that does not have a type.
