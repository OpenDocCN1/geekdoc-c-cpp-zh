# ISO/IEC 14882:2017(E)

Table 54 — Character traits requirements (continued)

| Expression | Return type | Assertion/note pre/post-condition | Complexity |
|---|---|---|---|
| X::to_int_type(c) | X::int_type | Returns: some value, constrained by the definitions of to_char_type and eq_int_type | constant |
| X::eq_int_type(e,f) | bool | Returns: for all c and d, X::eq(c,d) is equal to X::eq_int_type(X::to_int_type(c), X::to_int_type(d)); otherwise, yields true if e and f are both copies of X::eof(); otherwise, yields false if one of e is a copy of X::eof() and the other is not; otherwise the value is unspecified. | constant |
| X::eof() | X::int_type | Returns: a value such that X::eq_int_type(e,int_type(c)) is false for all values c. | constant |

The class template template<Char> struct traits; should be in the header <string> as a basis for explicit specializations.

# 24.2.2 Types typedefeds [char.traits.typedefs]

using char_type = CHAR_T;

+   1 The type for a certain container type char_type, a related container type INT_T shall be a type or class that can represent all of the valid characters converted from the corresponding char_type values, as well as an end-of-file value, EOF represents a container type which can hold end-of-file to be used as a return type of the lostream class member functions.224

+   2 using int_type = INT_T;

+   3 Requires Requirements for off_type and pos_type are described in 30.2.2 and 30.3.

using off_type = implementation-defined; using pos_type = implementation-defined;

+   4 using state_type = STATE_T;

+   Requires: state_type shall meet the requirements of CopyAssignable (Table 26), CopyConstructible (Table 24), and DefaultConstructible types.

> 224) If EOF can be held in char_type then some lostream operations may give surprising results.

§ 24.2.2

©ISO/IEC 2017 - All rights reserved 725