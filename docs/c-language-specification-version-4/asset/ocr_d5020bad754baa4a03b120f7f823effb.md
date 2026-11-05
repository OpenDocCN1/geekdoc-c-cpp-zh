# 14. Enums

An enum type is a distinct value type (§4.1) that declares a set of named constants.

The example

```
enum Color
{
    Red,
    Green,
    Blue
}
```

declares an enum type named Color with members Red, Green, and Blue.

# 14.1 Enum declarations

An enum declaration declares a new enum type. An enum declaration begins with the keyword enum, and defines the name, accessibility, underlying type, and members of the enum.

```
enum-declaration:
    attributes_opt enum-modifiers_opt enum identifier enum-base_opt enum-body ;_opt

enum-base:
    : integral-type

enum-body:
    { enum-member-declarations_opt }
    { enum-member-declarations , }
```

Each enum type has a corresponding integral type called the underlying type of the enum type. This underlying type must be able to represent all the enumerator values defined in the enumeration. An enum declaration may explicitly declare an underlying type of byte, sbyte, short, ushort, int, uint, long or ulong. Note that char cannot be used as an underlying type. An enum declaration that does not explicitly declare an underlying type has an underlying type of int.

The example

```
enum Color: long
{
    Red,
    Green,
    Blue
}
```

declares an enum with an underlying type of long. A developer might choose to use an underlying type of long, as in the example, to enable the use of values that are in the range of long but not in the range of int, or to preserve this option for the future.

# 14.2 Enum modifiers

An enum-declaration may optionally include a sequence of enum modifiers:

```
enum-modifiers:
    enum-modifier
    enum-modifiers enum-modifier
```