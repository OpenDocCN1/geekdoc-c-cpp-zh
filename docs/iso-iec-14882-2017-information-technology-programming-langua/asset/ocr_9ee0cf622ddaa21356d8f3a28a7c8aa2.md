# ISO/IEC 14882:2017(E)

types are required. A class T must be defined if:

+   (5.1) an object of type T is defined (6.1), or

+   (5.2) a non-static class data member of type T is defined (12.2), or

+   (5.3) T is used as the aligned object or array type in a new-expression (8.3.4), or

+   (5.4) an invalue-to-reference conversion is applied to give a value referring to an object of type T (7.1), or

+   (5.5) an expression is converted (either implicitly or explicitly) to type T (Clause 7, 7.2, 8.23, 8.27, 8.29, 8.4), or

+   (5.6) an expression that is not a null constant, and has other than void*, is converted to the type pointer to or reference to T using a standard conversion (Clause 7), a dynamic_cast (8.2.7) or a static_cast (8.2.9), or

+   (5.7) a class member access is applied to an expression of type T (8.2.5), or

+   (5.8) the typeid (8.2.8) or the sizeof (8.3.3) is applied to an operand of type T, or

+   (5.9) a function with a return type or argument type of type T is defined (6.1) or called (8.2.2), or

+   (5.10) a class with a base class of T is defined (Clause 13), or

+   (5.11) an instance of type T is assigned to (8.18), or

+   (5.12) the type of an expression (8.3.6), or pointer to T is

+   (5.13) an exception-declaration has reference to T, or pointer to T (18.3).

end note

6 There can be more than one definition of a class (Clause 12), inline template (10.2), inline function with external linkage (10.1.6), inline variable with external linkage (10.6), class template, non-static function template (17.5.6), static data member of a class template (17.5.7), member function of a class template (17.5.7.1), or template specialization for which some template parameters are not specified (17.7, 17.5.3) in a program where each definition appears in a translation unit, and all definitions satisfy the following requirements. Given such an entity D defined in more than one translation unit, then

+   (6.1) each definition of D shall consist of the same sequence of tokens;

+   (6.2) within each definition of D, corresponding names, looked up according to 6.4, shall refer to an entity defined within the definition of D, or refer to the same entity, after overload resolution (16.3) and matching of partial template specialization (17.8.3), except that a name can refer to

+   (6.2.1) a non-volatile object with internal or external linkage if the object is

+   (6.2.2) has the same type name in all definitions of D;

+   (6.2.3) is initialized with a constant expression (8.20),

+   (6.2.4) is not-odr in any definition of D, and

+   has the same value in all definitions of D;

or

+   (6.2.2) a reference with internal or no linkage initialized with a constant expression such that the reference refers to the same entity in all definitions of D;

and

+   (6.3) in each definition of D, corresponding entities shall have the same language linkage; and

+   (6.4) in each definition of D, the overloaded operators referred to, the implicit calls to the same function, or constructors, operator new functions and operator delete functions, refer to the same function, or to function defined within the operator and D;

§ 6.2 ©/IEC 2017 - All rights reserved 43