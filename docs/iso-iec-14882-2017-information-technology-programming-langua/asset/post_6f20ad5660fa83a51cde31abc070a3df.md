
# ISO/IEC 14882:2017(E)

```cpp
extern X anotherX; // declares anotherX
using N::; // declares d
// end example
```

+   [Note: In some circumstances, C++ implementations define the default constructor (15.1), copy constructor (15.8), copy assignment operator (15.8), move assignment operator (15.8), or destructor (15.4) member functions. — end note] [Example: Given

```cpp
#include <string>

struct C {
    std::string s; // std::string is the standard library class (Clause 24)
};

int main() {
    C a;
    C b = a;
    b = a;
}
```

the implementation will implicitly define functions to make the definition of C equivalent to
struct C {
    std::string s;
    C() : s() {}
    C(const C& x) : s(x.s) {} // : (static_cast<std::string&&>(x.s)) {}
    C(C&& x) : s(std::move(x.s)) {}
    C& operator=(const C& x) { s = x.s; return *this; }
    C& operator=(C&& x) { s = static_cast<std::string&&>(x.s); return *this; }
    ~C() // : std::move(x.s); return *this; }
}
// end example

+   [Note: A class name can also be implicitly declared by an elaborated-type specifier (10.1.7.3) — end note]

+   A program is ill-defined if the definition of any object gives the object an incomplete type (6.9).

# 6.2 One-definition rule [basic.def.odr]

No translation unit shall contain more than one definition of any variable, function, class type, enumeration or template.

An expression is evaluated unless it is an unvaluated expression (Clause 8) or a subexpression thereof. The set of potential results of an expression e is defined as follows:

+   If e is an id-expression (8.1.4), the set contains only e.

+   If e is a subscribing expression (8.2.1) with an array operand, the set contains the potential results of that operand.

+   If e is a class access expression (8.2.5), the set contains the potential results of the object expression.

+   If e is a pointer-to-member expression (8.5) whose second operand is a constant expression, the set contains the potential results of the expression.

+   If e has the form (e1), the set contains the potential results of e1.

+   If e is a conditional expression (8.16), the set is the union of the sets of potential results of the second and threads.

+   (2.7) — If **e** or **E** is a comma expression (8.19), the set contains the potential results of the right ordering.

+   (2.8) — Otherwise, the set is empty.

Note: This set is a (possibly-empty) set of id-expressions, each of which is either e or a subexpression of e.

*Example*: In the following example, the set of potential results of the initializer of n S:x subexpression, but not the first S:x subexpression:

```cpp
struct S {int x = 0;
const int x;
int n = b + x; // S:x is not od-used
(&S:x); // S:x is od-used here, so a definition is required
```
— end example

3 A variable x whose name appears as a potentially-evaluated expression ex is od-used unless ex applies a non-trivial value-to-expression conversion (7.1) to a constant expression (8.20) that does not involve any variable-value, and if x is an element of the set of potential results of an expression e, where either the value-to-expression conversion (7.1) is od-used if it appears as a potentially-evaluated expression (8.8) or as the result of an expression in the body of a non-static function (12.2.2). A virtual function is od-used if it appears as a potentially-evaluated expression (8.8) or as the result of a function call (15.5). A virtual function is not od-used if it is not the unique lookup or the selected member of an expression and if it forms a pointer to member (8.3.4), unless it is a pure function or virtual (6.4, 16.3) [Note: This covers calls to many overloaded functions (8.2.2), operator overload (Clause 16), user-defined-expression conversion (13.3), and implicit conversion (15.12) as non-default initialization (11.6)]. A constructor selected to initialize an object of type class is od-used by a new-expression appearing in a potentially-evaluated expression for a class is od-used by a new-expression (15.8). An allocation function for a class is od-used by a delete expression specified in 8.3.4 and 15.5. A deletion function for a class is od-used by a delete expression appearing in a potentially-evaluated expression as specified in 8.3.5 and 15.8. A constructor for a class is od-used by the destructor of that class, or by being selected by the lookup at the point of definition of a virtual destructor (15.4). An assignment operator in a class is od-used if it is called by an implicitly defined copy-assignment or move-assignment function for another class as specified in 15.8. A constructor for a class is od-used as specified in 11.6. A destructor for a class is od-used if it is potentially invoked (15.4).

4 Every program has exactly one definition of every non-function or variable that is od-used that outside of a discarded statement (9.4.1); no diagnostic required. The definition can appear explicitly in the code, and if it is found in the standard or a user-defined library, (where appropriate) it is implicitly defined (15.1, 15.4 and 15.8). An inline function or variable shall be defined in every translation unit in which it is od-used outside of a discarded statement.

5 Exactly one definition of a class is required in a translation unit if the class is used in a way that requires the type to be complete. [Example: The complete translation unit is well-formed, even though it defines X:

```cpp
struct X;
// declare x as a struct type
struct X *x;
// use x in pointer function
// use x in pointer function
```
— example] [Note: The rules for declarations and expressions describe in which contexts complete class types are required.

27 An implementation is not required to call allocation and deallocation functions from constructors or destructors; however, this is a permissible technique

A class T must be defined if:

+   (5.1) an object of type T is defined (6.1), or

+   (5.2) a non-static class data member of type T is defined (12.2), or

+   (5.3) T is used as the aligned object or array type in a new-expression (8.3.4), or

+   (5.4) an invalue-to-reference conversion is applied to give a value reference to type T, or

+   (5.5) an expression is converted (either implicitly or explicitly) to type T (Clause 7, 8.23, 8.9, 8.4), or

+   (5.6) a template for which some template parameters are not specified (17.7, 17.5.3) in a program where each definition appears in a translation unit, and all definitions satisfy the following requirements.

+   (5.7) a class access is applied to an expression of type T (8.2.5), or

+   (5.8) the typeid (8.8) or sizeof (8.3) is applied to operand of type T, or

+   (5.9) a function with return type or argument type of T is called (8.2), or

+   (5.10) a base class of T is defined (Clause 13), or

+   (5.11) an instance of type T is assigned to (8.18), or

+   (5.12) an exception-declaration has reference to T, or (18.3).

end note

6 There can be more than one definition of a class (Clause 12), inline template (10.2), inline function with external linkage (10.6), inline variable with external linkage (10.6), class template, non-static function template (17.5.6), static data member of a class template (17.5.7), member function of a class template (17.5.7), or template specialization for which some template parameters are not specified (17.7) in a program where each definition appears in a translation unit, and all definitions satisfy the following requirements. Given such an entity D in more than one translation unit, then

+   (6.1) each definition of D shall consist of the same sequence of tokens;

+   (6.2) within each definition of D, corresponding names, looked up according 6.4, shall refer to an entity defined within the definition of D, or refer to the same entity, after overload resolution (16.3) and matching of partial template specialization (17.8.3), except that a name can refer to

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

§ 6.2 ©ISO/IEC 2017 – All rights reserved 42
