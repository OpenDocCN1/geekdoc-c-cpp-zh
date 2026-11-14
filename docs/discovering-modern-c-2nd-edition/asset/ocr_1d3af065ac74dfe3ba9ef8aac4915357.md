A very special operator in C++ is the *Comma Operator* that provides a sequential evaluation. The meaning is simply evaluating first the subexpression to the left of the comma and then that to the right of it. The value of the whole expression is that of the right subexpression:

```
3 + 4, 7 * 9.3
```

The result of the expression is 65.1 and the computation of the first subexpression is entirely irrelevant in this case. The subexpressions can contain the comma operator as well so that arbitrarily long sequences can be defined. With the help of the comma operator, one can evaluate multiple expressions in program locations where only one expression is allowed. A typical example is the increment of multiple indices in a *for*-loop (§1.4.4.2):

```
++i, ++j
```

When used as a function argument, the comma expression needs surrounding parentheses; otherwise the comma is interpreted as separation of function arguments.

# 1.3.6 Memory Handling

The operators *new* and *delete* allocate and deallocate memory, respectively. We postpone their description to Section 1.8.2 since discussing these operators before talking about pointers makes no sense.

# 1.3.7 Access Operators

C++ provides several operators for accessing substructures, for referring—i.e., taking the address of a variable—and dereferencing—i.e., accessing the memory referred to by an address. They are listed in Table 1–6. We will demonstrate in Section 2.2.3 how to use them, after we introduce pointers and classes.

# Table 1–6: Access Operators

| Operation | Expression | Reference |
|---|---|---|
| Member selection | x.m | §2.2.3 |