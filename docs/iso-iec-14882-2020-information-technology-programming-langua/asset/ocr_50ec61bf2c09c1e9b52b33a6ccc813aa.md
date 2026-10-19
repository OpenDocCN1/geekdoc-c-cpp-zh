[Example 1: After
typedef int MILES, *KLICKSP;
the constructions
MILES distance;
extern KLICKSP metricp;
are all correct declarations; the type of distance is int and that of metricp is “pointer to int”. — end example]

2 A typedef-name can also be introduced by an alias-declaration. The identifier following the using keyword becomes a typedef-name and the optional attribute-specifier-seq following the identifier appertains to that typedef-name. Such a typedef-name has the same semantics as if it were introduced by the typedef specifier. In particular, it does not define a new type.

[Example 2:
using handler_t = void (*)(int);
extern handler_t ignore;
extern void (*ignore)(int);    // redeclar e ignore
using cell = pair<void*, cell*>;    // error
— end example]

The defining-type-specifier-seq of the defining-type-id shall not define a class or enumeration if the alias-declaration is the declaration of a template-declaration.

3 In a given non-class scope, a typedef specifier can be used to redeclare the name of any type declared in that scope to refer to the type to which it already refers.

[Example 3:
typedef struct s { /* ... */ } s;
typedef int I;
typedef int I;
typedef I I;
— end example]

4 In a given class scope, a typedef specifier can be used to redeclare any class-name declared in that scope that is not also a typedef-name to refer to the type to which it already refers.

[Example 4:
struct S {
    typedef struct A { } A;    // OK
    typedef struct B B;    // OK
    typedef A A;    // error
};
— end example]

5 If a typedef specifier is used to redeclare in a given scope an entity that can be referenced using an elaborated-type-specifier, the entity can continue to be referenced by an elaborated-type-specifier or as an enumeration or class name in an enumeration or class definition respectively.

[Example 5:
struct S;
typedef struct S S;
int main() {
    struct S* p;    // OK
}
struct S { };    // OK
— end example]

6 In a given scope, a typedef specifier shall not be used to redeclare the name of any type declared in that scope to refer to a different type.

[Example 6:
class complex { /* ... */ };
typedef int complex;    // error: redefinition
— end example]