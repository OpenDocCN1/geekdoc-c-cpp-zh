# ISO/IEC 14882:2017(E)

# 11.3.5 Functions

1 In a declaration T where D has the type D

```
D1 ( parameter-declaration-clause ) cv-qualifier-seq_opt
    ref-qualifier_opt noexcept-specifier_opt attribute-specifier-seq_opt
```

and the type of the declared-id in the declaration D1 is "derived-declarator-type-list T", the type of the declared-id in D is "derived-declarator-type-list noexcept_opt function of (parameter-declaration-clause) cv-qualifier-seq_opt ref-qualifier_opt returning T", where the optional noexcept is present if and only if the exception specification (18.4) is non-throwing. The optional attribute-specifier-seq pertains to the function type,

2 In a declaration D has the type D

```
D1 ( parameter-declaration-clause ) cv-qualifier-seq_opt
    ref-qualifier_opt noexcept-specifier_opt attribute-specifier-seq_opt trailing-return-type
```

and the type of the declared-id in the declaration D1 is "derived-declarator-type-list T", T shall be the simple-type declarator. The auto-type "derived-declarator-type-list noexcept_opt function of (parameter-declaration-clause) cv-qualifier-seq_opt ref-qualifier_opt returning U", where U is the type specified by the returning-type, and where the optional noexcept is present if and only if the exception specification is non-throwing. The optional attribute-specifier-seq pertains to the function type.

3 A type of other form is a function type [10]

```
parameter-declaration-clause:
    parameter-declaration-list : ...
    parameter-declaration-list , ...
    parameter-declaration-list:
    parameter-declaration
    parameter-declaration-list , parameter-declaration
    parameter-declaration:
    attribute-specifier-seq_opt decl-specifier-seq decl-specifier = initializer-clause
    attribute-specifier-seq_opt decl-specifier-seq abstract-declarator-list
    attribute-specifier-seq_opt decl-specifier-seq abstract-declarator-list_opt = initializer-clause
```

4 The parameter-declaration-clause determines what elements can be specified, and their processing, when the function is called. Note: The parameter-declaration-clause determines the elements specified on the function (see 6.2). If the parameter-declaration-clause is empty, the function takes no arguments. A parameter list consisting of a single unnamed parameter of non-dependent type void is equivalent to an empty parameter list. If the parameter-declaration-clause terminates with an ellipsis or a parameter pack (17.5.3), the number of arguments should be equal to or greater than the number of parameters that do not have a default argument and are not function packs. Syntactically correct and where " ... " is not part of an abstract-declarator, " ... " is synonymous with " ." . [Example: The declaration

```
int print(const char*);

declares a function that can be called with varying numbers and types of arguments.
printf("hello world\n");
printf("%ld = %ld\n", a, b);
```

However, the first argument must be of a type that can be converted to a const char* — end example][ Note: The standard header <cstdarg> contains a mechanism for passing arguments using the 100) As indicated by, cv-qualifiers are a significant component in function return types.

§ 11.3 ISO/IEC 2017 – All rights reserved 210