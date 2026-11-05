```
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

# B.2.9 Arrays

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

# B.2.10 Interfaces

```
interface-declaration:
  attributes_opt interface-modifiers_opt partial_opt interface
  identifier variant-type-parameter-list_opt interface-base_opt
  type-parameter-constraints-clauses_opt interface-body ;_opt

interface-modifiers:
  interface-modifier
  interface-modifiers interface-modifier
```