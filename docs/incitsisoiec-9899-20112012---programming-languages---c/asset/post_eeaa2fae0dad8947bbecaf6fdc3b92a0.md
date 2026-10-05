
# Semantics

3 A postfix expression followed by the . operator and an identifier designates a member of a structure or union object. The value is that of the named member, and if the first expression is an lvalue. If the first expression has qualified type, the result has the so-qualified version of the type of the designated member.

4 A postfix expression followed by the -> operator and an identifier designates a member of a structure or union object. The value is that of the named member of the object to which the first expression points, and is an lvalue. If the first expression is a pointer to a qualified type, the result has the so-qualified version of the type of the designated member.

5 Accessing a member of an atomic structure or union object results in undefined behavior.

6 One special guarantee is made in order to simplify the use of unions: if a union contains several structures that share a common initial sequence (below), and if a union object contains only one of these structures, it is permitted to inspect the common part of any of them anywhere where a declaration of the completed type of the union is visible. Two structures share a common initial sequence if corresponding members have compatible types (and, for bit-fields, the same widths) for a sequence of one or more members.

EXAMPLE 1 If f is a function returning a structure or union, and x is a member of that structure or union, f() is a valid postfix expression but not an lvalue.

EXAMPLE 2 In:

```
struct s { int i; const int ci; 
  struct s;
  const struct s cs;
  volatile struct vs;
```

the members have the types:

> 96 If & is a valid pointer expression where & is the "address-of-" which generates a pointer to its operand), the expression (&E)->MOS is the same as E.MOS.

> 97 For example, a data race would occur if access to the entire structure or union in one thread conflicts with access to a member from another, where at least one access is a modification. Members can be safely accessed using a non-atomic object which is assigned to or from the atomic object.

```
s.i int
s.ci const int
cs.i const int
cs.ci const int
vs.i volatile int
vs.ci volatile const int
```

EXAMPLE 3 The following is a valid fragment:

```
union {
  struct {
    int alltypes;
  } n;
  struct {
    int type;
    int intnode;
  } ni;
  struct {
    int type;
    double doublenode;
  } nf;
} u;
u.nf.type = 1;
u.nf.doublen = 3.14;
/* ... */
if (u.n.alltypes == 1)
  if (sin(u.nf.doublenode) == 0.0)
    /* ... */
```

The following is not a valid fragment (because the union type is not visible within function f):

```
struct t1 { int m; }
struct t2 { int m; };
int f(struct t1 *p1, struct t2 *p2)
{
  if (p1->m < 0)
    p2->m = -p2->m;
  return p1->m;
}
int g()
{
  union {
    struct t1 s1;
    struct t2 s2;
  } u;
  /* ... */
  return f(&u.s1, &u.s2);
}
```

**Forward references:** address and indirection operators (6.5.3.2), structure and union specifiers (6.7.2.1).

## 6.5.2.4 Postfix increment and decrement operators

## Constraints

+   The operand of the postfix increment or decrement operator shall have atomic, qualified, or unqualified reference or pointer type, and shall be a modifiable lvalue.

## Semantics

+   The result of the postfix ++ operator is the value of the operand. As a side effect, the value of the operand object is incremented (that is, the value 1 of the appropriate type is added to it). See the discussions of additive operators and compound assignment for information on constraints, types, and conversions and the effects of operations on pointers. The value computation of the result is sequenced before the side effect of updating the stored value of the operand. With respect to an indeterminately-sequenced function call, the operation of postfix ++ is a single evaluation. Postfix ++ on an object with atomic type is a read-modify-write operation with memory_order_seq_cst memory semantics.

+   The postfix -- operator is analogous to the postfix ++ operator, except that the value of the operand is decremented (that is, the value 1 of the appropriate type is subtracted from it).

Forward references: additive operators (6.5.6), compound assignment (6.5.16.2).

## 6.5.2.5 Compound literals

## Constraints

+   The type name shall specify a complete object type or an array of unknown size, but not a variable length array type.

+   All constraints for initializer lists in 6.7.9 also apply to compound literals.

## Semantics

+   A postfix expression that consists of a parenthesized type name followed by a brace-en list of initializers is a compound literal. It provides an unnamed object whose 

> Where a pointer to an atomic object can be formed and E has integer type, E++ is equivalent to the following code sequence where T is the type of E:

```
T *addr = &E;
T old = *addr;
T new;
do {
    new = old + 1;
} while (!atomic_compare_exchange_strong(addr, &old, new));
```

with old being the result of the operation.
Special care must be taken if E has floating point type; see 6.5.16.2.

value is given by the initializer list.99)

If the type name specifies an array of unknown size, the size is determined by the initializer list as specified in 6.7.9, and the type of the compound literal is that of the completed array. Otherwise (when the type name specifies an object type), the type of the compound literal is that specified by the type name. In either case, the result is an lvalue.

The value of the compound literal is that of an unnamed object initialized by the initializer list. If the compound literal occurs outside the body of the function, the object has static storage duration; otherwise, it has automatic storage duration associated with the enclosing block.

All the semantic rules for initializer lists in 6.7.9 also apply to compound literals.100)

String literals, and compound literals with const-qualified types, need not designate distinct objects.101)

## EXAMPLE 1 The file scope definition

```
int *p = (int []){2, 4};
```

initializes p to point to the first element of an array of two ints, the first having the value two and the second, four. The expressions in this compound literal are required to be constant. The unnamed object has static storage duration.

## EXAMPLE 2 In contrast,

```
void f(void)
{
    int *p;
    /*...*/
    p = (int [2]){*p};
    /*...*/
}
```

p is assigned the address of the first element of an array of two ints, the first having the value previously pointed to p and the second, zero. The expressions in this compound literal need not be constant. The unnamed object has automatic storage duration.

## EXAMPLE 3 Initializers with designations can be combined with compound literals. Structure objects created using compound literals can be passed to functions without depending on member order:

```
drawline((struct point){.x=1, .y=1},
       (struct point){.x=3, .y=4});
```

> 99 Note that this differs from a cast. For example, a cast specifies a conversion to scalar types only, and the result of such a cast is not an lvalue.

> 100 For example, this allows implementations to share storage for string literals and compound literals

> 101 This allows implementations to share storage for string literals and compound literals with overlapping representations.

Or, if drawline instead expected pointers to point:

```
drawline(&(struct point){.x=1, .y=1};
& (struct point){.x=3, .y=4});
```

EXAMPLE 4 A read-only literal can be specified through constructions like:

```
(const float j){1e0, 1e1, 1e2, 1e3, 1e4, 1e5, 1e6}
```

EXAMPLE 5 The three examples have different meanings:

```
"tmp/fileXXXXX"
(char j[])("/tmp/fileXXXXX"
(const char j[])("/tmp/fileXXXXX")
```

The first has static storage duration and has type array of char, which cannot be modifiable; the last have automatic storage duration when they occur within the body of a function, and first of these are modifiable.

EXAMPLE 6 Like strings, const-qualified compound literals can be placed into read-only memory and can even be shared. For example:

```
(const char j[])"abc" == "abc"
```

might yield 1.

EXAMPLE 7 Since compound literals are unnamed, a single compound literal cannot specify a circularly linked object. For example, there is no way to write a self-referential compound literal that could be used as the argument in place of the named object endless_zeros below:

```
struct int_list { int char; struct int_list *cdr };
struct int_list endless_zeros = {0,&endless_zeros};
eval (endless_zeros);
```

EXAMPLE 8 Each compound literal creates only a single object in a given scope:

```
struct s { int i };
```

The function f() always returns the value 1.

Note that if an iteration statement were used instead of an explicit goto and a labeled statement, the lifetime of the unnamed object would be the loop only, and on entry time around p would have an indeterminate value, which would result in undefined behavior.

Forward references: type names (6.7.7), initialization (6.7.9).
