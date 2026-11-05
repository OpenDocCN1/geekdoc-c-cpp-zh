```
: primary_no_array_creation_expression '[' argument_list ']'
;

// Source: $11.7.11 Null Conditional Element Access
null_conditional_element_access
  : primary_no_array_creation_expression '?' '[' argument_list ']'
dependent_access*
  ;

// Source: $11.7.12 This access
this_access
  : 'this'
  ;

// Source: $11.7.13 Base access
base_access
  : 'base' '.' identifier type_argument_list?
  | 'base' '[' argument_list ']'
  ;

// Source: $11.7.14 Postfix increment and decrement operators
post_increment_expression
  : primary_expression '++'
  ;

post_decrement_expression
  : primary_expression '--'
  ;

// Source: $11.7.15.2 Object creation expressions
object_creation_expression
  : 'new' type '(' argument_list? ')' object_or_collection_initializer?
  | 'new' type object_or_collection_initializer
  ;

object_or_collection_initializer
  : object_initializer
  | collection_initializer
  ;

// Source: $11.7.15.3 Object initializers
object_initializer
  : '{' member_initializer_list? '}'
  | '{' member_initializer_list ',' '}'
  ;

member_initializer_list
  : member_initializer (',' member_initializer)*
  ;

member_initializer
  : initializer_target '=' initializer_value
  ;

initializer_target
```