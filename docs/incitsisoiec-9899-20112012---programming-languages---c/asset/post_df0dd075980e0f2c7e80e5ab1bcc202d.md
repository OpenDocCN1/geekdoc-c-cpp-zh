
EXAMPLE 4 The rule limiting assignments between restricted pointers does not distinguish between a function call and with exception, only "outer-to-inner" assignments between restricted pointers declared in nested blocks have defined behavior.

```c
int * restrict p1;
int * restrict q1;
p1 = q1; // undefined behavior
{
    int * restrict p2 = p1; // valid
    int * restrict q2 = q1; // valid
    p1 = q2; // undefined behavior
    p2 = q2; // undefined behavior
}
```

The exception allows the value of a restricted pointer to be carried out of the block in which it (or, more precisely, the identifier used to designate it) is declared when block finishes execution. For example, this permits new_vector to return a vector.

```c
typedef struct { int n; float * restrict v; } vector;
vector new_vector(int n)
{
    vector t;
    t.n = n;
    t.v = malloc(n * sizeof(float));
    return t;
}
```

## 6.7.4 Function specifiers

### Syntax

```c
function-specifier:
inline
_Noturn
```

### Constraints

Function specifiers shall be used only in the declaration of an identifier for a function.

An inline definition of a function with external linkage shall not contain a definition of a modifiable object with static or thread storage duration, and shall not contain a reference to an identifier with internal linkage.

In a hosted environment, no function specifier(s) shall appear in a declaration of main.

### Semantics

A function specifier may appear more than once; the behavior is the same as if it appeared once.

A function declared with an inline function specifier is an inline function. Making an inline function suggests that calls to the function will be as fast as possible.

The extent to which such suggestions are effective is implementation-defined.¹³⁹

Any function with external linkage be an inline function. For a function with external-link, the following restrictions apply: If a function is declared with an **inline** function specifier, then it shall also be defined in the same translation unit. If all of the file declarations for a function in a translation unit include the **inline** function specifier without **extern**, then the definition in that translation unit is *inline*. An inline definition does not provide an external definition for the function, and does not forbid an external definition in another translation unit. An inline definition provides an alternative to an external definition, which a translator may use to implement any call to the function in the same translation unit. It is unspecified whether a call to the function uses the inline definition or the external definition.¹⁴⁰

A function declared with a `_noreturn` function specifier shall not return to its caller.

## **Recommended practice**

The implementation should produce a diagnostic message for a function declared with a `_Noreturn` function specifier that appears to be capable of returning to its caller.

EXAMPLE 1 The declaration of an inline function with external linkage can result in either an external definition, or a definition available for use only within the translation unit. A file scope declaration with **extern** creates an external definition. This example shows an entire translation unit.

```c
inline double f(double t)
{
    return (9.0 * t) / 5.0 + 32.0;
}
inline double cells(double t)
{
    return (5.0 * (t - 32.0)) / 9.0;
}
extern double jahr(double); // creates an external definition
```

138) By using, for example, an alternative to the usual function call mechanism, such as “inline substitution”. Inline substitution is not textual, nor does it create a new function. Therefore, for example, the expansion of a macro used within the body of the function uses the definition it had at the point the body appears, and not where the function is called; and identifiers refer to the declarations in scope where the body occurs. The function has a single address, regardless of the number of inline definitions that occur in addition to the external definition.

139) For example, an implementation might never perform inline substitution, or may only perform inline substitutions to the scope of an **inline** declaration.

140) Since an inline definition is distinct from the corresponding external definition and from any other inline definitions in other translation units, all corresponding objects with static storage duration are also distinct in each of the definitions.

```c
double convert (int is_fahr, double temp)
{
    /* A translator perform inline substitutions */
    return is_fahr ? cels(temp) : fahr(temp);
}
```

Note that the definition of fahr is an external definition because fahr is declared with extern, but the definition of cels is an inline definition. Because cels has external link and referenced, an external definition has to appear in another translation unit (see 6.9); the inline definition and the external definition are distinct and may be used for the call.

## EXAMPLE 2

```c
_Noturn void f () {
    abort(); // ok
}
_Noturn void g (int i) { // causes undefined behavior if i<=0
    if (i > 0) abort();
}
```

Forward references: function definitions (6.9.1).

## 6.7.5 Alignment experiment

### Syntax

```c
+ alignment-specifier:
__Alignas ( type-name ))
__Alignas ( constant-expression )
```

### Constraints

An alignment attribute shall not be specified in a declaration of a typedef, or a bit-field, or a function, or a parameter, or an object declared with the register storage duration.

An alignment attribute shall not be specified in a declaration of a typedef, or a bit-field, or a function, or a parameter, or an object declared with the register storage duration.

An alignment attribute shall not be specified in a declaration of a typedef, or a bit-field, or a function, or a parameter, or an object declared with the register storage duration.

### Semantics

An alignment attribute shall not be specified in a declaration of a typedef, or a bit-field, or a function, or a parameter, or an object declared with the register storage duration.

The constant expression shall be an integer expression. The alignment requirement of the object is to be specified by the alignment attributes in the same declaration.

If, in the declaration “**T D1**, **D1** has the form

```c
Alignas ( constant-expression )
```

then the ident has the type specified by the declaration “**T (constant-expression)**”. Thus, a declarator in parentheses is identical to the unparenthesized declarator, but the binding of complicated declarators may be altered by parentheses.

## 6.7.6 Declarators

### Syntax

```c
declarator:
    pointer_opt
direct-declarator:
    identifier
    ( declarator )
    direct-declarator [ expression-opt ]
direct-declarator [ static ]
direct-declarator ( parameter-type-list )
pointer:
    * type-qualifier-list_opt
type-qualifier-list:
    type-qualifier
    type-qualifier type-qualifier
parameter-type-list:
    parameter-list
    parameter-list , ...
```-list:

identifier-list:
    identifier
identifier-list , identifier
```

### Semantics

Each declarator declares one identifier, and asserts that when an operand of the same form as the declarator appears in an expression, it designates a function or object with the scope, storage duration, and type indicated by the declaration specifiers.

A declarator is a declarator that is not part of another declarator. The end of a full declarator is a sequence point. If, in the nested sequence of declarators in a full declarator, there is a declarator specifying a variable length type, the type specified by the full declarator is said to be *variably modified*. Furthermore, any type derived by declarator type from a variably modified type is itself variably modified.

In the following subclauses, consider a declaration

```c
T D1
```

where T contains the declaration specifiers that specify a type (such as **int**) and **D1** is a declarator that contains an identifier *ident*. The type specified for the identifier *ident* in the various forms of declarator is described inductively using this notation.

If, in the declaration “**T D1**, **D1** has the form

```c
ident
```

then the type specified for *ident* is *T*.

If, in the declaration “**T D1**, **D1** has the form

```c
( D )
```

then the ident has the type specified by the declaration “**T D**”. Thus, a declarator in parentheses is identical to the unparenthesized declarator, but the binding of complicated declarators may be altered by parentheses.

## Implementation limits

As discussed in 5.2.4.1, an implementation may limit the number of pointer, array, and function declarators that modify an arithmetic, structure, union, or **void** type, either directly or via one or more **typedefs**.
