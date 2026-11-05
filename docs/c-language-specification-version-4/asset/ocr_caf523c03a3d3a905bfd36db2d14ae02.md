```
operator-modifier:
    public
    static
    extern

operator-declarator:
    unary-operator-declarator
    binary-operator-declarator
    conversion-operator-declarator

unary-operator-declarator:
    type operator overloadable-unary-operator ( type identifier )

overloadable-unary-operator: one of
    +  -  !  ~  ++  --  true  false

binary-operator-declarator:
    type operator overloadable-binary-operator ( type identifier , type identifier )

overloadable-binary-operator:
    +
    -
    *
    /
    %
    &
    |
    ^
    <<
    right-shift
    ==
    !=
    >
    <
    >=
    <=

conversion-operator-declarator:
    implicit operator type ( type identifier )
    explicit operator type ( type identifier )

operator-body:
    block
    ;

constructor-declaration:
    attributesopt constructor-modifiersopt constructor-declarator constructor-body

constructor-modifiers:
    constructor-modifier
    constructor-modifiers constructor-modifier
```