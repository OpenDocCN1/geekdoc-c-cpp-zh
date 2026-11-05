# 8.3 Value types

# 8.3.1 General

A value type is either a struct type or an enumeration type. C# provides a set of predefined struct types called the simple types. The simple types are identified through keywords.

```
value_type
  : non_nullable_value_type
  | nullable_value_type
  ;

non_nullable_value_type
  : struct_type
  | enum_type
  ;

struct_type
  : type_name
  | simple_type
  ;

simple_type
  : numeric_type
  | 'bool'
  ;

numeric_type
  : integral_type
  | floating_point_type
  | 'decimal'
  ;

integral_type
  : 'sbyte'
  | 'byte'
  | 'short'
  | 'ushort'
  | 'int'
  | 'uint'
  | 'long'
  | 'ulong'
  | 'char'
  ;

floating_point_type
  : 'float'
  | 'double'
  ;

enum_type
  : type_name
  ;

nullable_value_type
```