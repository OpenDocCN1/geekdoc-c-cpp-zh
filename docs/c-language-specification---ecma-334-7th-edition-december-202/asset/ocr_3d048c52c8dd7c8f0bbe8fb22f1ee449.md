```
// Source: §14.6 Namespace member declarations
namespace_member_declaration
  : namespace_declaration
  | type_declaration
  ;

// Source: §14.7 Type declarations
type_declaration
  : class_declaration
  | struct_declaration
  | interface_declaration
  | enum_declaration
  | delegate_declaration
  ;

// Source: §14.8.1 General
qualified_alias_member
  : identifier ':' identifier type_argument_list?
  ;

// Source: §15.2.1 General
class_declaration
  : attributes? class_modifier* 'partial'? 'class' identifier
    type_parameter_list? class_base? type_parameter_constraints_clause*
    class_body ';'?
  ;

// Source: §15.2.2.1 General
class_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'abstract'
  | 'sealed'
  | 'static'
  | unsafe_modifier  // unsafe code support
  ;

// Source: §15.2.3 Type parameters
type_parameter_list
  : '<' type_parameters '>'
  ;

type_parameters
  : attributes? type_parameter
  | type_parameters ',' attributes? type_parameter
  ;

// Source: §15.2.4.1 General
class_base
  : ':' class_type
  | ':' interface_type_list
  | ':' class_type ',' interface_type_list
```