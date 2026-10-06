# ISO/IEC 14882:2017(E)

3 A variable declaration with an inline specifier declares an inline variable.

4 A function defined within a class definition is an inline function.

5 The inline specifier should not appear in a block scope declaration. 94 If the inline specifier is used in a friend function declaration, that declaration shall be a definition or the function shall have previously been inline.

6 An inline function or variable shall be defined in every translation unit in which it is used-and shall have exactly the same definition in every case (6.2). [Note: A call to the inline function or use of the inline variable may be encountered before its definition in the translation unit.—end note.] If the definition of a function or variable in a translation unit before its first declaration as inline, the program is ill-formed. If a function or variable with external linkage is declared in one translation unit, it shall be declared in all translation units in which it appears; no diagnostic is required. [Note: A static local variable in an inline function with external linkage refers to the same object. A definition of the body of an inline function with external linkage is the same type in every translation unit.—end note].

# 10.1.7 Type specifiers

+   1 The type-specifiers are [dcl.type]

```
type-specifier:
  simple-type-specifier
  elaborated-type-specifier
  cv-typename
  cv-qualifier
type-specifier-seq:
  type-specifier attribute-specifier-seq,opt
  type-specifier type-specifier-seq
defining-type-specifier:
  type-specifier
  class
  enum
defefining-type-specifier-seq:
  defining-type-specifier attribute-specifier-seq,opt
  defining-type-specifier defining-type-specifier-seq
```

The optional attribute-specifier-seq in a type-specifier or a defining-type-specifier-seq pertains to the type denoted by the preceding type-specifiers or defining-type-specifiers (11.3). The attribute-specifier affects only the type for which it appears, not other declarations involving the same type.

+   2 As a general rule, at most one defining-type-specifier is allowed in the complete dcl-specifier-seq of a declaration or in a defining-type-specifier-seq, and at most one type-specifier is allowed in a type-specifier-seq. The exceptions to this rule are:

+   (2.1) const can be combined with any type specifier except itself.

+   (2.2) volatile can be combined with any type specifier except itself.

+   (2.3) signed or unsigned can be combined with char, long, short, or int.

+   (2.4) short or long can be combined with int.

+   (2.5) long can be combined with double.

+   (2.6) long can be combined with long.

> 94 The inline keyword has no effect on the linkage of a function.

§ 10.1.7 ©ISO/IEC 2017 – All rights reserved 165