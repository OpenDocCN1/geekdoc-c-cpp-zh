# 14. Enums

An enum type is a distinct value type (§4.1) that declares a set of named constants.

> JON SKEET Notably, these “named constants” are effectively just numbers. They cannot express behavior, contrary to almost everything else in C#. This is one of the very few areas where Java is more expressive than C#. In Java, enums have a lot more power: An enum can declare methods and then override them for specific values, for example. While it’s possible to emulate some of the features of Java enums within C#, language (and framework) support in a future version would be extremely welcome.

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

# 14.1 Enum Declarations

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