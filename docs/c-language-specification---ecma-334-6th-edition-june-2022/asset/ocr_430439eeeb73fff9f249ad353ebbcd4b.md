```
// Source: $11.20 Constant expressions
constant_expression
  : expression
  ;

// Source: $11.21 Boolean expressions
boolean_expression
  : expression
  ;

// Source: $12.1 General
statement
  : labeled_statement
  | declaration_statement
  | embedded_statement
  ;

embedded_statement
  : block
  | empty_statement
  | expression_statement
  | selection_statement
  | iteration_statement
  | jump_statement
  | try_statement
  | checked_statement
  | unchecked_statement
  | lock_statement
  | using_statement
  | yield_statement
  | unsafe_statement    // unsafe code support
  | fixed_statement     // unsafe code support
  ;

// Source: $12.3.1 General
block
  : '{' statement_list? '}'
  ;

// Source: $12.3.2 Statement lists
statement_list
  : statement+
  ;

// Source: $12.4 The empty statement
empty_statement
  : ';'
  ;

// Source: $12.5 Labeled statements
labeled_statement
  : identifier ':' statement
  ;

// Source: $12.6.1 General
```