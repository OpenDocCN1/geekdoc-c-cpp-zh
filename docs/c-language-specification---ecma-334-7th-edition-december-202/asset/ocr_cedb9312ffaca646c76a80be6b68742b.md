```
; 
attribute_list
  : attribute (',' attribute)*
  ;

attribute
  : attribute_name attribute_arguments?
  ;

attribute_name
  : type_name
  ;

attribute_arguments
  : '(' positional_argument_list? ')'
  | '(' positional_argument_list ',' named_argument_list ')'
  | '(' named_argument_list ')'
  ;

positional_argument_list
  : positional_argument (',' positional_argument)*
  ;

positional_argument
  : argument_name? attribute_argument_expression
  ;

named_argument_list
  : named_argument (',' named_argument)*
  ;

named_argument
  : identifier '=' attribute_argument_expression
  ;

attribute_argument_expression
  : expression
  ;
```

For the production global_attribute_target, and in the text below, identifier shall have a spelling equal to assembly or module, where equality is that defined in §6.4.3. For the production attribute_target, and in the text below, identifier shall have a spelling that is not equal to assembly or module, using the same definition of equality as above.

An attribute consists of an attribute_name and an optional list of positional and named arguments. The positional arguments (if any) precede the named arguments. A positional argument consists of an attribute_argument_expression; a named argument consists of a name, followed by an equal sign, followed by an attribute_argument_expression, which, together, are constrained by the same rules as simple assignment. The order of named arguments is not significant.

Note: For convenience, a trailing comma is allowed in a global_attribute_section and an attribute_section, just as one is allowed in an array_initializer (§17.7). end note

The attribute_name identifies an attribute class.