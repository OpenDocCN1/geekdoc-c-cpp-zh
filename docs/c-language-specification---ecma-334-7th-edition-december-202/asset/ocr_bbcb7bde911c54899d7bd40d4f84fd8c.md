Both signatures are reserved, even if the indexer is read-only or write-only.

Furthermore the member name Item is reserved.

# 15.3.10.5 Member names reserved for finalizers

For a class containing a finalizer (§15.13), the following signature is reserved:

```
void Finalize();
```

# 15.4 Constants

A constant is a class member that represents a constant value: a value that can be computed at compile-time. A constant_declaration introduces one or more constants of a given type.

```
constant_declaration
: attributes? constant_modifier* 'const' type constant_declarators ';'
;
```

```
constant_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
;
```

A constant_declaration may include a set of attributes (§22), a new modifier (§15.3.5), and any one of the permitted kinds of declared accessibility (§15.3.6). The attributes and modifiers apply to all of the members declared by the constant_declaration. Even though constants are considered static members, a constant_declaration neither requires nor allows a static modifier. It is an error for the same modifier to appear multiple times in a constant declaration.

The type of a constant_declaration specifies the type of the members introduced by the declaration. The type is followed by a list of constant_declarators (§13.6.3), each of which introduces a new member. A constant_declarator consists of an identifier that names the member, followed by an "=" token, followed by a constant_expression (§12.23) that gives the value of the member.

The type specified in a constant declaration shall be sbyte, byte, short, ushort, int, uint, long, ulong, char, float, double, decimal, bool, string, an enum_type, or a reference_type. Each constant_expression shall yield a value of the target type or of a type that can be converted to the target type by an implicit conversion (§10.2).

> Note: Examples of such constructs include case labels, goto case statements, enum member declarations, attributes, and other constant declarations. end note

> Note: As described in §12.23, a constant_expression is an expression that can be fully evaluated at compile-time. Since the only way to create a non-null value of a reference_type other than string is