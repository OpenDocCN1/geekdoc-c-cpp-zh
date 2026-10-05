EXAMPLE 4 The rule limiting assignments between restricted pointers does not distinguish between a function call and with exception, only "outer-to-inner" assignments between restricted pointers declared in nested blocks have defined behavior.

```
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

```
typedef struct { int n; float * restrict v; } vector;
vector new_vector(int n)
{
    vector t;
    t.n = n;
    t.v = malloc(n * sizeof(float));
    return t;
}
```

# 6.7.4 Function specifiers

# Syntax

```
function-specifier:
inline
_Noturn
```

# Constraints

Function specifiers shall be used only in the declaration of an identifier for a function.

An inline definition of a function with external linkage shall not contain a definition of a modifiable object with static or thread storage duration, and shall not contain a reference to an identifier with internal linkage.

In a hosted environment, no function specifier(s) shall appear in a declaration of main.

# Semantics

A function specifier may appear more than once; the behavior is the same as if it appeared once.

A function declared with an inline function specifier is an inline function. Making an inline function suggests that calls to the function will be as fast as possible.