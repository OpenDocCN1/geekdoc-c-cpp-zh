```
// Source: §13.11 The try statement
try_statement
  : 'try' block catch_clauses
  | 'try' block catch_clauses? finally_clause
  ;

catch_clauses
  : specific_catch_clause+
  | specific_catch_clause* general_catch_clause
  ;

specific_catch_clause
  : 'catch' exception_specifier exception_filter? block
  | 'catch' exception_filter block
  ;

exception_specifier
  : '(' type identifier? ')'
  ;

exception_filter
  : 'when' '(' boolean_expression ')'
  ;

general_catch_clause
  : 'catch' block
  ;

finally_clause
  : 'finally' block
  ;

// Source: §13.12 The checked and unchecked statements
checked_statement
  : 'checked' block
  ;

unchecked_statement
  : 'unchecked' block
  ;

// Source: §13.13 The lock statement
lock_statement
  : 'lock' '(' expression ')' embedded_statement
  ;

// Source: §13.14 The using statement
using_statement
  : 'using' '(' resource_acquisition ')' embedded_statement
  ;

resource_acquisition
  : local_variable_declaration
  | expression
```