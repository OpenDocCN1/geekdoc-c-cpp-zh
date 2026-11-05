```
{
}

*end example*
```

# 21.2.4 Attribute parameter types

The types of positional and named parameters for an attribute class are limited to the attribute parameter types, which are:

+   - One of the following types: `bool`, `byte`, `char`, `double`, `float`, `int`, `long`, `sbyte`, `short`, `string`, `uint`, `ulong`, `ushort`.
+   - The type `object`.
+   - The type `System.Type`.
+   - Enum types.
+   - Single-dimensional arrays of the above types.
+   - A constructor argument or public field that does not have one of these types, shall not be used as a positional or named parameter in an attribute specification.

# 21.3 Attribute specification

Attribute specification is the application of a previously defined attribute to a program entity. An attribute is a piece of additional declarative information that is specified for a program entity. Attributes can be specified at global scope (to specify attributes on the containing assembly or module) and for type_declarations (§13.7), class_member_declarations (§14.3), interface_member_declarations (§17.4), struct_member_declarations (§15.3), enum_member_declarations (§18.2), accessor_declarations (§14.7.3), event_accessor_declarations (§14.8), elements of formal_parameter_lists (§14.6.2), and elements of type_parameter_lists (§14.2.3).

Attributes are specified in attribute sections. An attribute section consists of a pair of square brackets, which surround a comma-separated list of one or more attributes. The order in which attributes are specified in such a list, and the order in which sections attached to the same program entity are arranged, is not significant. For instance, the attribute specifications [A][B], [B][A], [A, B], and [B, A] are equivalent.

```
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
```