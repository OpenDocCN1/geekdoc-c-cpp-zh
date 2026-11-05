# B. Grammar

```
    argument:
        argument-name_opt  argument-value

    argument-name:
        identifier :

    argument-value:
        expression
        ref variable-reference
        out variable-reference

    primary-expression:
        primary-no-array-creation-expression
        array-creation-expression

    primary-no-array-creation-expression:
        literal
        simple-name
        parenthesized-expression
        member-access
        invocation-expression
        element-access
        this-access
        base-access
        post-increment-expression
        post-decrement-expression
        object-creation-expression
        delegate-creation-expression
        anonymous-object-creation-expression
        typeof-expression
        checked-expression
        unchecked-expression
        default-value-expression
        anonymous-method-expression

    simple-name:
        identifier type-argument-list_opt

    parenthesized-expression:
        ( expression )
```