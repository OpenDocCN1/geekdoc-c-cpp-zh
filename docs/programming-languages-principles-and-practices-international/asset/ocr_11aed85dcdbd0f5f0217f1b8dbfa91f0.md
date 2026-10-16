# 8.2 Simple Types

Algol-like languages (C, Ada, Pascal), including the object-oriented ones (C++, Java), all classify data types according to a relatively standard basic scheme, with minor variations. Unfortunately, the names used in different language definitions are often different, even though the concepts are the same. We will attempt to use a generic name scheme in this section and then point out differences among some of the foregoing languages in the next.

Every language comes with a set of predefined types from which all other types are constructed. These are generally specified using either keywords (such as int or double in C++ or Java) or predefined identifiers (such as String or Process in Java). Sometimes variations on basic types are also predefined, such as short, long, long double, unsigned int, and so forth that typically give special properties to numeric types.

Predefined types are primarily simple types: types that have no other structure than their inherent arithmetic or sequential structure. All the foregoing types except String and Process are simple. However, there are simple types that are not predefined: enumerated types and subrange types are also simple types.

Enumerated types are sets whose elements are named and listed explicitly. A typical example (in C) is

```
enum Color {Red, Green, Blue};
```

or (the equivalent in Ada):

```
type Color_Type is (Red, Green, Blue);
```

or (the equivalent in ML):

```
datatype Color_Type = Red | Green | Blue;
```

In Ada and ML, enumerations are defined in a type declaration, and are truly new types. In most languages (but not ML), enumerations are ordered, in that the order in which the values are listed is important. Also, most languages include a predefined successor and predecessor operation for any enumerated type. Finally, in most languages, no assumptions are made about how the listed values are represented internally, and the only possible value that can be printed is the value name itself. As a runnable example, the short program in Figure 8.1 demonstrates Ada’s enumerated type mechanism, which comes complete with symbolic I/O capability so that the actual defined names can be printed. In particular, see line 6, which allows enumeration values to be printed.

```
(1) with Text_IO; use Text_IO;
(2) with Ada.Integer_Text_IO; use Ada.Integer_Text_IO;

(3) procedure Enum is
(4)   type Color_Type is (Red,Green,Blue);
(5)   -- define Color_IO so that Color_Type values can be -- printed
(6)   package Color_IO is new Enumeration_IO(Color_Type);
(7)   use Color_IO;
```

Figure 8.1 An Ada program demonstrating the use of an enumerated type (continues)