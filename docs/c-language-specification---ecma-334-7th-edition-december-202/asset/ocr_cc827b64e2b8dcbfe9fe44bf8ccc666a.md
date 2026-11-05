```
overloadable_binary_operator
  : '+' | '-' | '*' | '/' | '%' | '&' | '|' | '^' | '<<'
  | right_shift | '==' | '!=' | '>' | '<' | '>=' | '<='
  ;

conversion_operator_declarator
  : 'implicit' 'operator' type '(' fixed_parameter ')'
  | 'explicit' 'operator' type '(' fixed_parameter ')'
  ;

operator_body
  : block
  | '=>' expression ';'
  | ';'
  ;

// Source: §15.11.1 General
constructor_declaration
  : attributes? constructor_modifier* constructor_declarator constructor_body
  ;

constructor_modifier
  : 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'extern'
  | unsafe_modifier  // unsafe code support
  ;

constructor_declarator
  : identifier '(' formal_parameter_list? ')' constructor_initializer?
  ;

constructor_initializer
  : ':' 'base' '(' argument_list? ')'
  | ':' 'this' '(' argument_list? ')'
  ;

constructor_body
  : block
  | '=>' expression ';'
  | ';'
  ;

// Source: §15.12 Static constructors
static_constructor_declaration
  : attributes? static_constructor_modifiers identifier '(' ')'
    static_constructor_body
  ;

static_constructor_modifiers
  : 'static'
  | 'static' 'extern' unsafe_modifier?
  | 'static' unsafe_modifier 'extern'?
  ;
```