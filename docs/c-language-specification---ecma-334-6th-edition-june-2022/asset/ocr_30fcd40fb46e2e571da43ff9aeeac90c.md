An enum declaration that does not explicitly declare an underlying type has an underlying type of int.

*Example: The example*

```
enum Color: long
{
    Red,
    Green,
    Blue
}
```

declares an enum with an underlying type of long.

*end example*

*Note: A developer might choose to use an underlying type of long, as in the example, to enable the use of values that are in the range of long but not in the range of int, or to preserve this option for the future. end note*

*Note: C# allows a trailing comma in an enum_body, just like it allows one in an array_initializer (§16.7). end note*

An enum declaration cannot include a type parameter list, but any enum nested inside a generic class declaration or a generic struct declaration is a generic enum declaration, since type arguments for the containing type shall be supplied to create a constructed type (§8.4).

# 18.3 Enum modifiers

An enum_declaration may optionally include a sequence of enum modifiers:

```
enum_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
;
```

It is a compile-time error for the same modifier to appear multiple times in an enum declaration. The modifiers of an enum declaration have the same meaning as those of a class declaration (§14.2.2). However, the abstract, and sealed, and static modifiers are not permitted in an enum declaration. Enums cannot be abstract and do not permit derivation.

# 18.4 Enum members

The body of an enum type declaration defines zero or more enum members, which are the named constants of the enum type. No two enum members can have the same name.

```
enum_member_declarations
: enum_member_declaration (',' enum_member_declaration)*
;

enum_member_declaration
: attributes? identifier ('=' constant_expression)?
;
```