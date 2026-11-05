Primary expressions are divided between array-creation-expressions and primary-no-array-creation-expressions. Treating array-creation-expression in this way, rather than listing it along with the other simple expression forms, enables the grammar to disallow potentially confusing code such as

```
object o = new int[3][1];
```

which would otherwise be interpreted as

```
object o = (new int[3])[1];
```

# 7.6.1 Literals

A primary-expression that consists of a literal (§2.4.4) is classified as a value.

# 7.6.2 Simple Names

A simple-name consists of an identifier, optionally followed by a type argument list:

```
simple-name:
    identifier type-argument-list_opt
```

A simple-name is either of the form I or of the form I<A1 ... Ak>, where I is a single identifier and <A1, ..., Ak> is an optional type-argument-list. When no type-argument-list is specified, consider k to be zero. The simple-name is evaluated and classified as follows:

+   - If k is zero and the simple-name appears within a block, and if the block's (or an enclosing block's) local variable declaration space (§3.3) contains a local variable, parameter, or constant with name I, then the simple-name refers to that local variable, parameter, or constant and is classified as a variable or value.
+   - If k is zero and the simple-name appears within the body of a generic method declaration and if that declaration includes a type parameter with name I, then the simple-name refers to that type parameter.

> VLADIMIR RESHETNIKOV This rule also applies if the simple-name appears within a constructor-initializer and matches a name of the containing constructor's parameter.

> VLADIMIR RESHETNIKOV This condition always leads to a compile-time error later.