# 18.6 The fixed Statement

In an unsafe context, the embedded-statement (§8) production permits an additional construct, the fixed statement, which is used to “fix” a movable variable such that its address remains constant for the duration of the statement.

```
    embedded-statement:
        ...
        fixed-statement

    fixed-statement:
        fixed ( pointer-type fixed-pointer-declarators ) embedded-statement

    fixed-pointer-declarators:
        fixed-pointer-declarator
        fixed-pointer-declarators , fixed-pointer-declarator

    fixed-pointer-declarator:
        identifier = fixed-pointer-initializer

    fixed-pointer-initializer:
        & variable-reference
        expression
```

Each fixed-pointer-declarator declares a local variable of the given pointer-type and initializes that local variable with the address computed by the corresponding fixed-pointer-initializer. A local variable declared in a fixed statement is accessible in any fixed-pointer-initializers occurring to the right of that variable’s declaration, and in the embedded-statement of the fixed statement. A local variable declared by a fixed statement is considered read-only. A compile-time error occurs if the embedded statement attempts to modify this local variable (via assignment or the ++ and -- operators) or pass it as a ref or out parameter.

A fixed-pointer-initializer can be one of the following:

+   * The token “&” followed by a variable-reference (§5.3.3) to a movable variable (§18.3) of an unmanaged type T, provided the type T* is implicitly convertible to the pointer type given in the fixed statement. In this case, the initializer computes the address of the given variable, and the variable is guaranteed to remain at a fixed address for the duration of the fixed statement.
+   
+   * An expression of an array-type with elements of an unmanaged type T, provided the type T* is implicitly convertible to the pointer type given in the fixed statement. In this case, the initializer computes the address of the first element in the array, and the entire array is guaranteed to remain at a fixed address for the duration of the fixed statement. The