```
member_access
  : primary_expression '.' identifier type_argument_list?
  | predefined_type '.' identifier type_argument_list?
  | qualified_alias_member '.' identifier type_argument_list?
  ;

predefined_type
  : 'bool' | 'byte' | 'char' | 'decimal' | 'double' | 'float' | 'int'
  | 'long' | 'object' | 'sbyte' | 'short' | 'string' | 'uint' | 'ulong'
  | 'ushort'
  ;

// Source: §12.8.8 Null Conditional Member Access
null_conditional_member_access
  : primary_expression '?' '.' identifier type_argument_list?
    dependent_access*
  ;

dependent_access
  : '.' identifier type_argument_list?    // member access
  | '[' argument_list ']'    // element access
  | '(' argument_list? ')'    // invocation
  ;

null_conditional_projection_initializer
  : primary_expression '?' '.' identifier type_argument_list?
  ;

// Source: §12.8.9.1 General
invocation_expression
  : primary_expression '(' argument_list? ')'
  ;

// Source: §12.8.10 Null Conditional Invocation Expression
null_conditional_invocation_expression
  : null_conditional_member_access '(' argument_list? ')'
  | null_conditional_element_access '(' argument_list? ')'
  ;

// Source: §12.8.11.1 General
element_access
  : primary_no_array_creation_expression '[' argument_list ']'
  ;

// Source: §12.8.12 Null Conditional Element Access
null_conditional_element_access
  : primary_no_array_creation_expression '?' '[' argument_list ']'
    dependent_access*
  ;

// Source: §12.8.13 This access
this_access
  : 'this'
  ;
```