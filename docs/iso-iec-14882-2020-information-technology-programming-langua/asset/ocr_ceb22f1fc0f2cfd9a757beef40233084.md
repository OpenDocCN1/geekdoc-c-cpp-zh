# ISO/IEC 14882:2020(E)

conversion-function-id:
    operator conversion-type-id
conversion-type-id:
    type-specifier-seq conversion-declarator_opt
conversion-declarator:
    ptr-operator conversion-declarator_opt
base-clause:
    : base-specifier-list
base-specifier-list:
    base-specifier ..._opt
    base-specifier-list , base-specifier ..._opt
base-specifier:
    attribute-specifier-seq_opt class-or-decltype
    attribute-specifier-seq_opt virtual access-specifier_opt class-or-decltype
    attribute-specifier-seq_opt access-specifier virtual_opt class-or-decltype
class-or-decltype:
    nested-name-specifier_opt type-name
    nested-name-specifier template simple-template-id
    decltype-specifier
access-specifier:
    private
    protected
    public
ctor-initializer:
    : mem-initializer-list
mem-initializer-list:
    mem-initializer ..._opt
    mem-initializer-list , mem-initializer ..._opt
mem-initializer:
    mem-initializer-id ( expression-list_opt )
    mem-initializer-id braced-init-list
mem-initializer-id:
    class-or-decltype
    identifier

# A.10 Overloading

[gram.over]

operator-function-id:
    operator operator
operator: one of
    new      delete    new[]    delete[]  co_await  ()        []        ->        ->*
    ~        !         +        -         *         /         %         ^         &
    |        =         +=       -=        *=        /=        %=        ^=        &=
    |=       ==        !=       <         >         <=        >=        <= >       &&
    ||       <<        >>       <<=       >>=       ++        --        ,

literal-operator-id:
    operator string-literal identifier
    operator user-defined-string-literal

# A.11 Templates

[gram.temp]

template-declaration:
    template-head declaration
    template-head concept-definition
template-head:
    template < template-parameter-list > requires-clause_opt