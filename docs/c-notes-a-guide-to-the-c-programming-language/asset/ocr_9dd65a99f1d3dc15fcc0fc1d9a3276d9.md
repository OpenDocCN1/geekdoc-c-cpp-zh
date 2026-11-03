```
arithmetic-expr ==
    { integer-expr | floating-expr }

integer-expr =
    { integer-arithmetic-expr
    | bitwise-expr
    | logical-expr
    | pointer-difference
    | object-size-value
    | integer-cast-expr
    | integer-primary
    }

integer-arithmetic-expr =
    { [ + | - ] integer-expr
    | integer-expr [ + | - | * | / | % ] integer-expr
    }

bitwise-expr =
    { ~ integer-expr
    | integer-expr [ & | | | ^ | << | >> ]
        integer-expr
    }

pointer-difference =
    pointer-expr - pointer-expr

object-size-value =
    sizeof { expr | ( type-expr ) }

logical-expr =
    { logical-expr && logical-expr
    | logical-expr || logical-expr
    | ! logical-expr
    | expr [ == | != | = | > | < | >= | <= | = / = ] expr
    | expr % interpreted as (expr != 0)
    | ( logical-expr )
    }

integer-cast-expr ==
    ( { char | short | unsigned | long | opt int } ) arithmetic-expr

floating-expr =
    { floating-expr [ + | - | * | / ] floating-expr
    | [ + | - ] floating-expr
    | floating-cast-expr
    | floating-primary }
```