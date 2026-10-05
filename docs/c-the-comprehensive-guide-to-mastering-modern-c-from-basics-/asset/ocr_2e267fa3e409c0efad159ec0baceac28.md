The following list illustrates the subtle but important differences in usage together with pointers * and references &:

+   * int const val
The int value val is immutable.

+   * MyClass const &obj
All data fields and methods in MyClass, of which obj is an object, are immutable.

+   * int const * p_int
The int value pointed to by the pointer is immutable.

+   * int * const p_int
The pointer p_int is immutable; the int value is mutable.

+   * char const * const cstr
Both the content and the pointer are immutable.

As a mnemonic, one could say that const always marks the entity as immutable behind which it stands. In the much more common notation, where const is mentioned first, you must mentally “move” the leading const one position to the right. The following notations are equivalent:

+   * const int val and int const val

+   * const MyClass &obj and MyClass const &obj

+   * const int * p_int and int const * p_int

+   * char star * const cstr and char const * const cstr

You have already learned in Chapter 4, Section 4.2

# 13.10.1 Const Parameters