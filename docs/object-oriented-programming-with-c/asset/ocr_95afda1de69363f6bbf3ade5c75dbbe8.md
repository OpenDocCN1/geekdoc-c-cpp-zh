![](bbox=[0.248, 0.089, 0.751, 0.374])

Block2 is contained in block1. Note that a declaration in an inner block *hides* a declaration of the same variable in an outer block and, therefore, each declaration of **x** causes it to refer to a different data object. Within the inner block, the variable **x** will refer to the data object declared therein.

In C, the global version of a variable cannot be accessed from within the inner block. C++ resolves this problem by introducing a new operator called the *scope resolution operator*. This can be used to uncover a hidden variable. It takes the following form:

```
```cpp
:: variable-name
```
```

This operator allows access to the global version of a variable. For example, `::count` means the global version of the variable count (and not the local variable count declared in that block). Program 3.1 illustrates this feature.

# Program 3.1 — Scope Resolution Operator