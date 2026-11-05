In an unsafe context, the *primary-no-array-creation-expression* (§12.7) and *unary-expression* (§12.8) productions permit the following additional constructs:

```
```text
primary-no-array-creation-expression:
    ...
    pointer-member-access
    pointer-element-access

unary-expression:
    ...
    pointer-indirection-expression
    addressof-expression
```
```

These constructs are described in the following subclauses.

> > [Note: The precedence and associativity of the unsafe operators is implied by the grammar. end note]

# ### 23.6.2 Pointer indirection

*A pointer-indirection-expression* consists of an asterisk (`*`)followed by a *unary-expression*.

```
```text
pointer-indirection-expression:
    * unary-expression
```
```

The unary `*` operator denotes pointer indirection and is used to obtain the variable to which a pointer points. The result of evaluating `*P`, where P is an expression of a pointer type `T*`, is a variable of type T. It is a compile-time error to apply the unary `*` operator to an expression of type `void*` or to an expression that isn't of a pointer type.

The effect of applying the unary `*` operator to a `null` pointer is implementation-defined. In particular, there is no guarantee that this operation throws a `System.NullReferenceException`.

If an invalid value has been assigned to the pointer, the behavior of the unary `*` operator is undefined.

> > [Note: Among the invalid values for dereferencing a pointer by the unary `*` operator are an address inappropriately aligned for the type pointed to (see example in §23.5), and the address of a variable after the end of its lifetime. end note]

For purposes of definite assignment analysis, a variable produced by evaluating an expression of the form `*P` is considered initially assigned (§10.4.2).

# ### 23.6.3 Pointer member access

*A pointer-member-access* consists of a *primary-expression*, followed by a `"->"` token, followed by an *identifier* and an optional *type-argument-list*.

```
```text
pointer-member-access:
    primary-expression -> identifier type-argument-list_opt
```
```

In a pointer member access of the form `P->I`, P shall be an expression of a pointer type, and I shall denote an accessible member of the type to which P points.

A pointer member access of the form `P->I` is evaluated exactly as `(*P).I`. For a description of the pointer indirection operator (`*`), see §23.6.2. For a description of the member access operator (`.`), see §12.7.5.

> > [Example: In the following code

```
```csharp
using System;
struct Point
{
    public int x;
    public int y;
```
```