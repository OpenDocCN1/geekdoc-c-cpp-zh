+   - This value also becomes the result of the operation.

The ++ and -- operators also support postfix notation (§12.7.10). Typically, the result of x++ or x-- is the value of x *before* the operation, whereas the result of ++x or --x is the value of x *after* the operation. In either case, x itself has the same value after the operation.

An operator ++ or operator -- implementation can be invoked using either postfix or prefix notation. It is not possible to have separate operator implementations for the two notations.

Lifted (§12.4.8) forms of the unlifted predefined prefix increment and decrement operators defined above are also predefined.

# ### 12.8.7 Cast expressions

A *cast-expression* is used to convert explicitly an expression to a given type.

```
cast-expression:
    ( type ) unary-expression
```

A *cast-expression* of the form (T)E, where T is a *type* and E is a *unary-expression*, performs an explicit conversion (§11.3) of the value of E to *type* T. If no explicit conversion exists from E to T, a binding-time error occurs. Otherwise, the result is the value produced by the explicit conversion. The result is always classified as a value, even if E denotes a variable.

The grammar for a *cast-expression* leads to certain syntactic ambiguities. [Example: The expression (x)–y could either be interpreted as a *cast-expression* (a cast of –y to *type* x) or as an *additive-expression* combined with a *parenthesized-expression* (which computes the value x – y). end example]

To resolve *cast-expression* ambiguities, the following rule exists: A sequence of one or more *tokens* (§7.4) enclosed in parentheses is considered the start of a *cast-expression* only if at least one of the following are true:

+   - The sequence of tokens is correct grammar for a *type*, but not for an *expression*.
+   - The sequence of tokens is correct grammar for a *type*, and the token immediately following the closing parentheses is the token “~”, the token “!”, the token “(”, an *identifier* (§7.4.3), a *literal* (§7.4.5), or any *keyword* (§7.4.4) except **as** and **is**.

The term “correct grammar” above means only that the sequence of tokens shall conform to the particular grammatical production. It specifically does not consider the actual meaning of any constituent identifiers. [Example: If x and y are identifiers, then x.y is correct grammar for a *type*, even if x.y doesn’t actually denote a type. end example]

[Note: From the disambiguation rule, it follows that, if x and y are identifiers, (x)y, (x)(y), and (x)(-y) are *cast-expressions*, but (x)-y is not, even if x identifies a type. However, if x is a keyword that identifies a predefined type (such as int), then all four forms are *cast-expressions* (because such a keyword could not possibly be an expression by itself). end note]

# ### 12.8.8 Await expressions

# #### 12.8.8.1 General

The *await* operator is used to suspend evaluation of the enclosing *async* function until the asynchronous operation represented by the operand has completed.

```
await-expression:
    await unary-expression
```

An *await-expression* is only allowed in the body of an *async* function (§15.15). Within the nearest enclosing *async* function, an *await-expression* shall not occur in these places:

+   - Inside a nested (*non-async*) anonymous function