# ISO/IEC 14882:2017(E)

operators functions, and the categories of values you expect and yield are determined by the parameter and return types. — end note —

2 The result of a prvalue is a value the expression stores into its context. A prvalue result is the value V is sometimes to have name or the value V. *result object* of a prvalue is the object initialized by the prvalue; a prvalue that is used to compute the value of an operand of an operator or has type cv void has no result. [Note: Except when the prvalue is the operand of a *decltype-specifier*, a prvalue of class or array type always has a result. For a discarded prvalue, a temporary object is destroyed; Clause 8. — end note —] the result of a gluon is given by the entity described.

3 [Note: When in a context where a prvalue is expected, the gluon is converted to a prvalue; 7.1, 7.2, and 7.3. An attempt to bind a reference to an invalue is not such; 11.6.3] [Note: There are no prvalue-fields; if a bit-field is converted to a prvalue (7.1), a prvalue of the type of the bit-field is created, which might be promoted (7.6). — end note —]

[Note: When a prvalue appears in a context where a gluon is expected, the gluon is converted to an invalue: 7.4. — end note —]

5 The discussion of inference in 11.6.3 and of temporaries in 15.2 describes the behavior of gluvalues and in other contexts.

6 Unless otherwise indicated (8.2.2), a prvalue shall always have complete or incomplete non-void type. A class or array type shall not have cv. [Note: A gluon may have incomplete or non-void type. Class and array types may have cv-qualified types; otherwise arrays always have cv-unqualified types. Clause 8. — end note —]

7 An invalue is to access the stored value of an object through a gluon of other type. A program may attempt to modify an object through a nonmodifiable gluon expression or through an invalue expression is (8.18, 8.2, 8.3). — end note —

8 If a program accesses the stored value of an object through a gluon of other one of the following types the behavior is defined:⁵⁶

+   (8.1) a cv-qualified version of the dynamic type of the object.

+   (8.2) a dynamic type of the dynamic type of the object,

+   (8.3) a type similar (as defined in 7.5) to the dynamic type of the object,

+   (8.4) a type that is the signed or unsigned type corresponding to the cv-qualified version of the dynamic type of the object,

+   (8.6) an aggregate or union that includes one of the aforementioned types among its elements or non-static data members (including, recursively, an element or non-static data member of a subaggregate or contained union

+   (8.7) a type that is (possibly cv-qualified) base class of the dynamic type of the object,

+   (8.8) a char, unsigned char, and std:: :byte type.

# 6.11 [basic.align]

Object types have alignment (6.9.1, 6.9.2) which place restrictions on the addresses at which an object of type may be allocated. An alignment is an implementation-defined integer value representing the number of bytes between successive addresses at which an object can be allocated. An object imposes an alignment requirement on every object of that type; stricter alignment can be requested using the alignment specifier (10.6.2).

> 56 The intent of this list is to specify these circumstances in which an object may or not be aligned.

§ 6.11 ISO/IEC 2017 – All rights reserved 84