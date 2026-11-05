

| 'extern' 'static' unsafe_modifier?
| 'extern' unsafe_modifier 'static'
| unsafe_modifier 'static' 'extern'?
| unsafe_modifier 'extern' 'static'
;

static_constructor_body
: block
| '=>' expression ';'
| ';'
;

// 来源：§15.13 终结器
finalizer_declaration
: attributes? '~' identifier '(' ')' finalizer_body
| attributes? 'extern' unsafe_modifier? '~' identifier '(' ')'
finalizer_body
| attributes? unsafe_modifier 'extern'? '~' identifier '(' ')'
finalizer_body
;

finalizer_body
: block
| '=>' expression ';'
| ';'
;

// 来源：§16.2.1 一般
struct_declaration
: attributes? struct_modifier* 'ref'? 'partial'? 'struct'
identifier type_parameter_list? struct_interfaces?
type_parameter_constraints_clause* struct_body ';'?
;

// 来源：§16.2.2 结构体修饰符
struct_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
| 'readonly'
| unsafe_modifier   // 不安全代码支持
;

// 来源：§16.2.5 结构体接口
struct_interfaces
: ':' interface_type_list
;

// 来源：§16.2.6 结构体主体
struct_body
: '{' struct_member_declaration* '}'
;

// 来源：§16.3 结构体成员
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
  | fixed_size_buffer_declaration  // 不安全代码支持
  ;

// 来源：§17.7 数组初始化器
array_initializer
  : '{' variable_initializer_list? '}'
  | '{' variable_initializer_list ',' '}'
  ;

variable_initializer_list
  : variable_initializer (',' variable_initializer)*
  ;

variable_initializer
  : expression
  | array_initializer
  ;

// 来源：§18.2.1 一般
interface_declaration
  : attributes? interface_modifier* 'partial'? 'interface'
    identifier variant_type_parameter_list? interface_base?
    type_parameter_constraints_clause* interface_body ';'?
  ;

// 来源：§18.2.2 接口修饰符
interface_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | unsafe_modifier  // 不安全代码支持
  ;

// 来源：§18.2.3.1 一般
variant_type_parameter_list
  : '<' variant_type_parameters '>'
  ;

// 来源：§18.2.3.1 一般
variant_type_parameters
  : attributes? variance_annotation? type_parameter
| variant_type_parameters ',' attributes? variance_annotation?
type_parameter
;

// 来源：§18.2.3.1 一般
variance_annotation
: 'in'
| 'out'
;

// 来源：§18.2.4 基接口
interface_base
: ':' interface_type_list
;

// 来源：§18.3 接口主体
interface_body
: '{' interface_member_declaration* '}'
;

// 来源：§18.4.1 一般
interface_member_declaration
: interface_method_declaration
| interface_property_declaration
| interface_event_declaration
| interface_indexer_declaration
;

// 来源：§18.4.2 接口方法
interface_method_declaration
: attributes? 'new'? return_type interface_method_header
| attributes? 'new'? ref_kind ref_return_type interface_method_header
;

interface_method_header
: identifier '(' formal_parameter_list? ')' ';'
| identifier type_parameter_list '(' formal_parameter_list? ')'
type_parameter_constraints_clause* ';'
;

// 来源：§18.4.3 接口属性
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
;

// 来源：§18.4.4 接口事件
interface_event_declaration
  : attributes? 'new'? 'event' type identifier ';'
  ;

// 来源：§18.4.5 接口索引器
interface_indexer_declaration
  : attributes? 'new'? type 'this' '[' formal_parameter_list ']'
    '{' interface_accessors '}'
  | attributes? 'new'? ref_kind type 'this' '[' formal_parameter_list ']'
    '{' ref_interface_accessor '}'
  ;

// 来源：§19.2 枚举声明
enum_declaration
  : attributes? enum_modifier* 'enum' identifier enum_base? enum_body ';'?
  ;

enum_base
  : ':' integral_type
  | ':' integral_type_name
  ;

integral_type_name
  : type_name // 应解析为除 char 以外的整型类型
  ;

enum_body
  : '{' enum_member_declarations? '}'
  | '{' enum_member_declarations ',' '}'
  ;

// 来源：§19.3 枚举修饰符
enum_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  ;

// 来源：§19.4 枚举成员
enum_member_declarations
  : enum_member_declaration (',' enum_member_declaration)*
  ;

// 来源：§19.4 枚举成员
enum_member_declaration
  : attributes? identifier ('=' constant_expression)?
  ;

// 来源：§20.2 委托声明
delegate_declaration
: attributes? delegate_modifier* 'delegate' return_type delegate_header
| attributes? delegate_modifier* 'delegate' ref_kind ref_return_type
delegate_header
;

delegate_header
: identifier '(' formal_parameter_list? ')' ';'
| identifier variant_type_parameter_list '(' formal_parameter_list? ')'
type_parameter_constraints_clause* ';'
;

delegate_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
| unsafe_modifier  // 不安全代码支持
;

// 来源：§22.3 特性规范
global_attributes
: global_attribute_section+
;

global_attribute_section
: '[' global_attribute_target_specifier attribute_list ']'
| '[' global_attribute_target_specifier attribute_list ',' ']'
;

global_attribute_target_specifier
: global_attribute_target ':'
;

global_attribute_target
: identifier
;

attributes
: attribute_section+
;

attribute_section
: '[' attribute_target_specifier? attribute_list ']'
| '[' attribute_target_specifier? attribute_list ',' ']'
;

attribute_target_specifier
: attribute_target ':'
;

attribute_target
: identifier
| keyword
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

## A.4 不安全代码的语法扩展

// 来源：§23.2 不安全上下文
unsafe_modifier
  : 'unsafe'
  ;

unsafe_statement
  : 'unsafe' block
  ;

// 来源：§23.3 指针类型
pointer_type
  : value_type ('*')+
  | 'void' ('*')+
;

// 来源：§23.6.2 指针间接引用
pointer_indirection_expression
  : '*' unary_expression
  ;

// 来源：§23.6.3 指针成员访问
pointer_member_access
  : primary_expression '->' identifier type_argument_list?
  ;

// 来源：§23.6.4 指针元素访问
pointer_element_access
  : primary_no_array_creation_expression '[' expression ']'
  ;

// 来源：§23.6.5 取地址运算符
addressof_expression
  : '&' unary_expression
  ;

// 来源：§23.7 fixed 语句
fixed_statement
  : 'fixed' '(' pointer_type fixed_pointer_declarators ')' embedded_statement
  ;

fixed_pointer_declarators
  : fixed_pointer_declarator (',' fixed_pointer_declarator)*
  ;

fixed_pointer_declarator
  : identifier '=' fixed_pointer_initializer
  ;

fixed_pointer_initializer
  : '&' variable_reference
  | expression
  ;

// 来源：§23.8.2 固定大小缓冲区声明
fixed_size_buffer_declaration
  : attributes? fixed_size_buffer_modifier* 'fixed' buffer_element_type fixed_size_buffer_declarators ';'
  ;

fixed_size_buffer_modifier
  : 'new'
  | 'public'
  | 'internal'
  | 'private'
  | 'unsafe'
  ;

buffer_element_type

