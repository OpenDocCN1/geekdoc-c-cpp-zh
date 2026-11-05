

```
constructor-declarator:
    identifier ( formal-parameter-list_opt ) constructor-initializer_opt

constructor-initializer:
    : base ( argument-list_opt )
    : this ( argument-list_opt )

constructor-body:
    block
    ;

static-constructor-declaration:
    attributes_opt static-constructor-modifiers identifier ( ) static-constructor-body

static-constructor-modifiers:
    extern_opt static
    static extern_opt

static-constructor-body:
    block
    ;

destructor-declaration:
    attributes_opt extern_opt ~ identifier ( ) destructor-body

destructor-body:
    block
    ;
```

### B.2.8 结构体

```
struct-declaration:
    attributes_opt struct-modifiers_opt partial_opt struct identifier type-parameter-list_opt
    struct-interfaces_opt type-parameter-constraints-clauses_opt struct-body ;_opt

struct-modifiers:
    struct-modifier
    struct-modifiers struct-modifier

struct-modifier:
    new
    public
    protected
    internal
    private

struct-interfaces:
    : interface-type-list

struct-body:
    { struct-member-declarations_opt }

struct-member-declarations:
    struct-member-declaration
    struct-member-declarations struct-member-declaration

struct-member-declaration:
    constant-declaration
    field-declaration
    method-declaration
    property-declaration
    event-declaration
    indexer-declaration
    operator-declaration
    constructor-declaration
    static-constructor-declaration
    type-declaration
```

### B.2.9 数组

```
array-type:
    non-array-type rank-specifiers

non-array-type:
    type

rank-specifiers:
    rank-specifier
    rank-specifiers rank-specifier

rank-specifier:
    [ dim-separators_opt ]

dim-separators:
    ,
    dim-separators ,

array-initializer:
    { variable-initializer-list_opt }
    { variable-initializer-list , }

variable-initializer-list:
    variable-initializer
    variable-initializer-list , variable-initializer

variable-initializer:
    expression
    array-initializer
```

### B.2.10 接口

```
interface-declaration:
    attributes_opt interface-modifiers_opt partial_opt interface
    identifier variant-type-parameter-list_opt interface-base_opt
    type-parameter-constraints-clauses_opt interface-body ;_opt

interface-modifiers:
    interface-modifier
    interface-modifiers interface-modifier

interface-modifier:
    new
    public
    protected
    internal
    private

variant-type-parameter-list:
    < variant-type-parameters >

variant-type-parameters:
    attributes_opt variance-annotation_opt type-parameter
    variant-type-parameters , attributes_opt variance-annotation_opt type-parameter

variance-annotation:
    in
    out

interface-base:
    : interface-type-list

interface-body:
    { interface-member-declarations_opt }

interface-member-declarations:
    interface-member-declaration
    interface-member-declarations interface-member-declaration

interface-member-declaration:
    interface-method-declaration
    interface-property-declaration
    interface-event-declaration
    interface-indexer-declaration

interface-method-declaration:
    attributes_opt new_opt return-type identifier type-parameter-list
    ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;

interface-property-declaration:
    attributes_opt new_opt type identifier { interface-accessors }

interface-accessors:
    attributes_opt get ;
    attributes_opt set ;
    attributes_opt get ; attributes_opt set ;
    attributes_opt set ; attributes_opt get ;

interface-event-declaration:
    attributes_opt new_opt event type identifier ;

interface-indexer-declaration:
    attributes_opt new_opt type this [ formal-parameter-list ] { interface-accessors }
```

### B.2.11 枚举

```
enum-declaration:
    attributes_opt enum-modifiers_opt enum identifier enum-base_opt enum-body ;_opt

enum-base:
    : integral-type

enum-body:
    { enum-member-declarations_opt }
    { enum-member-declarations , }

enum-modifiers:
    enum-modifier
    enum-modifiers enum-modifier

enum-modifier:
    new
    public
    protected
    internal
    private

enum-member-declarations:
    enum-member-declaration
    enum-member-declarations , enum-member-declaration

enum-member-declaration:
    attributes_opt identifier
    attributes_opt identifier = constant-expression
```

### B.2.12 委托

```
delegate-declaration:
    attributes_opt delegate-modifiers_opt delegate return-type
    identifier variant-type-parameter-list_opt
        ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;

delegate-modifiers:
    delegate-modifier
    delegate-modifiers delegate-modifier

delegate-modifier:
    new
    public
    protected
    internal
    private
```

### B.2.13 特性

```
global-attributes:
    global-attribute-sections

global-attribute-sections:
    global-attribute-section
    global-attribute-sections global-attribute-section

global-attribute-section:
    [ global-attribute-target-specifier attribute-list ]
    [ global-attribute-target-specifier attribute-list , ]

global-attribute-target-specifier:
    global-attribute-target :

global-attribute-target:
    assembly
    module

attributes:
    attribute-sections

attribute-sections:
    attribute-section
    attribute-sections attribute-section

attribute-section:
    [ attribute-target-specifier_opt attribute-list ]
    [ attribute-target-specifier_opt attribute-list , ]

attribute-target-specifier:
    attribute-target :

attribute-target:
    field
    event
    method
    param
    property
    return
    type

attribute-list:
    attribute
    attribute-list , attribute

attribute:
    attribute-name attribute-arguments_opt

attribute-name:
    type-name

attribute-arguments:
    ( positional-argument-list )
    ( positional-argument-list , named-argument-list )
    ( named-argument-list )

positional-argument-list:
    positional-argument
    positional-argument-list , positional-argument

positional-argument:
    argument-name_opt attribute-argument-expression

named-argument-list:
    named-argument
    named-argument-list , named-argument

named-argument:
    identifier = attribute-argument-expression

attribute-argument-expression:
    expression
```

## B.3 不安全代码的语法扩展

```
class-modifier:
    ...
    unsafe

struct-modifier:
    ...
    unsafe

interface-modifier:
    ...
    unsafe

delegate-modifier:
    ...
    unsafe

field-modifier:
    ...
    unsafe

method-modifier:
    ...
    unsafe

property-modifier:
    ...
    unsafe

event-modifier:
    ...
    unsafe

indexer-modifier:
    ...
    unsafe

operator-modifier:
    ...
    unsafe

constructor-modifier:
    ...
    unsafe

destructor-declaration:
    attributes_opt extern_opt unsafe_opt ~ identifier ( ) destructor-body
    attributes_opt unsafe_opt extern_opt ~ identifier ( ) destructor-body

static-constructor-modifiers:
    extern_opt unsafe_opt static
    unsafe_opt extern_opt static
    extern_opt static unsafe_opt
    unsafe_opt static extern_opt
    static extern_opt unsafe_opt
    static unsafe_opt extern_opt

embedded-statement:
    ...
    unsafe-statement
    fixed-statement

unsafe-statement:
    unsafe block

type:
    ...
    pointer-type

pointer-type:
    unmanaged-type *
    void *

unmanaged-type:
    type

primary-no-array-creation-expression:
    ...
    pointer-member-access
    pointer-element-access
    sizeof-expression

unary-expression:
    ...
    pointer-indirection-expression
    addressof-expression

pointer-indirection-expression:
    * unary-expression

pointer-member-access:
    primary-expression -> identifier type-argument-list_opt

pointer-element-access:
    primary-no-array-creation-expression [ expression ]

addressof-expression:
    & unary-expression

sizeof-expression:
    sizeof ( unmanaged-type )

fixed-statement:
    fixed ( pointer-type fixed-pointer-declarators ) embedded-statement

fixed-pointer-declarators:
    fixed-pointer-declarator
    fixed-pointer-declarators , fixed-pointer-declarator

fixed-pointer-declarator:
    identifier = fixed-pointer-initializer
```

