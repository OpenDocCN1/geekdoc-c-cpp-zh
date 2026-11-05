+   - There is no concept of an “automatically implemented indexer”. It is an error to have a non-abstract, non-external indexer with semicolon accessors.

Aside from these differences, all rules defined in §15.7.3, §15.7.5 and §15.7.6 apply to indexer accessors as well as to property accessors.

> Note: This replacing of property/properties with indexer/indexers when reading §15.7.3, §15.7.5 and §15.7.6 applies to defined terms as well. For example read-write property becomes read-write-indexer. end note

# 15.10 Operators

# 15.10.1 General

An operator is a member that defines the meaning of an expression operator that can be applied to instances of the class. Operators are declared using operator_declarations:

```
operator_declaration
  : attributes? operator_modifier+ operator_declarator operator_body
  ;

operator_modifier
  : 'public'
  | 'static'
  | 'extern'
  | unsafe_modifier  // unsafe code support
  ;

operator_declarator
  : unary_operator_declarator
  | binary_operator_declarator
  | conversion_operator_declarator
  ;

unary_operator_declarator
  : type 'operator' overloadable_unary_operator '(' fixed_parameter ')'
  ;

overloadable_unary_operator
  : '+' | '-' | '!' | '~' | '++' | '--' | 'true' | 'false'
  ;

binary_operator_declarator
  : type 'operator' overloadable_binary_operator
    '(' fixed_parameter ',' fixed_parameter ')'
  ;

overloadable_binary_operator
  : '+' | '-' | '*' | '/' | '%' | '&' | '|' | '^' | '<<'
  | right_shift | '==' | '!=' | '>' | '<' | '>=' | '<='
  ;

conversion_operator_declarator
  : 'implicit' 'operator' type '(' fixed_parameter ')'
  | 'explicit' 'operator' type '(' fixed_parameter ')'
```