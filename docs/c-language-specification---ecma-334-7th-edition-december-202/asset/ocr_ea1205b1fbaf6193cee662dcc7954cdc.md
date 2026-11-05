```
| event_declaration
| indexer_declaration
| operator_declaration
| constructor_declaration
| finalizer_declaration
| static_constructor_declaration
| type_declaration
;

// Source: §15.4 Constants
constant_declaration
  : attributes? constant_modifier* 'const' type constant_declarators ';'
  ;

constant_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  ;

// Source: §15.5.1 General
field_declaration
  : attributes? field_modifier* type variable_declarators ';'
  ;

field_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'static'
  | 'readonly'
  | 'volatile'
  | unsafe_modifier  // unsafe code support
  ;

variable_declarators
  : variable_declarator (',' variable_declarator)*
  ;

variable_declarator
  : identifier ('=' variable_initializer)?
  ;

// Source: §15.6.1 General
method_declaration
  : attributes? method_modifiers return_type method_header method_body
  | attributes? ref_method_modifiers ref_kind ref_return_type method_header
    ref_method_body
  ;

method_modifiers
```