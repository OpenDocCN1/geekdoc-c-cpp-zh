# 15.5 Fields

# 15.5.1 General

A field is a member that represents a variable associated with an object or class. A field_declaration introduces one or more fields of a given type.

```
field_declaration
  : attributes? field_modifier* type variable_declarators ';'
  ;
```

```
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
```

```
variable_declarators
  : variable_declarator (',' variable_declarator)*
  ;
```

```
variable_declarator
  : identifier ('=' variable_initializer)?
  ;
```

unsafe_modifier (§23.2) is only available in unsafe code (§23).

A field_declaration may include a set of attributes (§22), a new modifier (§15.3.5), a valid combination of the four access modifiers (§15.3.6), and a static modifier (§15.5.2). In addition, a field_declaration may include a readonly modifier (§15.5.3) or a volatile modifier (§15.5.4), but not both. The attributes and modifiers apply to all of the members declared by the field_declaration. It is an error for the same modifier to appear multiple times in a field_declaration.

The type of a field_declaration specifies the type of the members introduced by the declaration. The type is followed by a list of variable_declarators, each of which introduces a new member. A variable_declarator consists of an identifier that names that member, optionally followed by an “=” token and a variable_initializer (§15.5.6) that gives the initial value of that member.

The type of a field shall be at least as accessible as the field itself (§7.5.5).

The value of a field is obtained in an expression using a simple_name (§12.8.4), a member_access (§12.8.7) or a base_access (§12.8.14). The value of a non-readonly field is modified using an assignment (§12.21).

The value of a non-readonly field can be both obtained and modified using postfix increment and decrement operators (§12.8.15) and prefix increment and decrement operators (§12.9.6).

A field declaration that declares multiple fields is equivalent to multiple declarations of single fields with the same attributes, modifiers, and type.

Example: