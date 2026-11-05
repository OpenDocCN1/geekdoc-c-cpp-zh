```
// Source: §15.3 Struct members
struct_member_declaration
: constant_declaration
| field_declaration
| method_declaration
| property_declaration
| event_declaration
| indexer_declaration
| operator_declaration
| constructor_declaration
| static_constructor_declaration
| type_declaration
| fixed_size_buffer_declaration    // unsafe code support
;

// Source: §16.7 Array initializers
array_initializer
: '{' variable_initializer_list? '}'
| '{' variable_initializer_list ',' '}'

variable_initializer_list
: variable_initializer (',' variable_initializer)*
;

variable_initializer
: expression
| array_initializer
;

// Source: §17.2.1 General
interface_declaration
: attributes? interface_modifier* 'partial'? 'interface'
identifier variant_type_parameter_list? interface_base?
type_parameter_constraints_clause* interface_body ';'?
;

// Source: §17.2.2 Interface modifiers
interface_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
| unsafe_modifier    // unsafe code support
;

// Source: §17.2.3.1 General
variant_type_parameter_list
: '<' variant_type_parameters '>'
;

// Source: §17.2.3.1 General
variant_type_parameters
```