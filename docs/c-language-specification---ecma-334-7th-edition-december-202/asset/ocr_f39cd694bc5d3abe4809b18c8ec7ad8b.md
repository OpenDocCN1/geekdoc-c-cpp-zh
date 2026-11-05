```
| variant_type_parameters ',' attributes? variance_annotation?
type_parameter
;

// Source: §18.2.3.1 General
variance_annotation
: 'in'
| 'out'
;

// Source: §18.2.4 Base interfaces
interface_base
: ':' interface_type_list
;

// Source: §18.3 Interface body
interface_body
: '{' interface_member_declaration* '}'
;

// Source: §18.4.1 General
interface_member_declaration
: interface_method_declaration
| interface_property_declaration
| interface_event_declaration
| interface_indexer_declaration
;

// Source: §18.4.2 Interface methods
interface_method_declaration
: attributes? 'new'? return_type interface_method_header
| attributes? 'new'? ref_kind ref_return_type interface_method_header
;

interface_method_header
: identifier '(' formal_parameter_list? ')' ';'
| identifier type_parameter_list '(' formal_parameter_list? ')'
type_parameter_constraints_clause* ';'
;

// Source: §18.4.3 Interface properties
interface_property_declaration
: attributes? 'new'? type identifier '{' interface_accessors '}'
| attributes? 'new'? ref_kind type identifier '{' ref_interface_accessor '}'
;

interface_accessors
: attributes? 'get' ';'
| attributes? 'set' ';'
| attributes? 'get' ';' attributes? 'set' ';'
| attributes? 'set' ';' attributes? 'get' ';'
;

ref_interface_accessor
: attributes? 'get' ';'
```