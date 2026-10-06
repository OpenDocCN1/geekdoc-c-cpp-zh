# ISO/IEC 14882:2017(E)

3 See also 8.18 and 11.6.

4 [Note: Forming a pointer to reference type is ill-formed; see 11.3.2. Forming a function pointer type is ill-formed if the function type has cv-qualifiers or a re-qualifier; see 11.3.5. Since the address of a bit-field (12.2.4) cannot be taken, a pointer can never point to a bit-field. — end note]

# 11.3.2 References [dcl:ref]

+   1 In a declaration T where D has either of the
```
&attribute-specifier-seq D1
&attribute-specifier-seq D2
```\and the type of the identifier in the declaration T D1 is *derived-declarator-type reference list to T*. The optional attribute-specifier-seq appertain to the reference type. CV-qualified references are ill-formed except when cv-qualifiers are introduced through a typedef name (10.1.3, 17.1), in which case the cv-qualifiers are ignored. Except Example:
```
defype int A;
const A ref = 3; // ill-formed: reference to non-const initialized with value
```

The type of are is "value reference to int", not "value reference to const int". — end example] [Note: A reference can be thought of as a name of an object. — end note] A declarator that specifies the type using & is "reference to cv void" is ill-formed.

+   2 A reference type that is declared using & is called an *ival reference*, and a reference type that is declared using & is called a *value reference*. Value references and reference types are distinct. Except where explicitly noted, they are semantically equivalent and commonly referred to as references.

+   3 [Example:
```
 f(double a) (a == 3.14);
//
double d = 0;
f(d);
```
declare a to be a reference parameter of f so the call f(d) will add 3.14 to d.
int v[20];
//...
int& g(int i) { return v[i]; }
//...
g(3) = 7;
```
declare the function g() to return a reference to an integer so g(3)=7 will assign 7 to the fourth element of the array v. For another example,
```
struct link {
link* next;
};
link* first;
void h(link& p) { // p is a reference to pointer
p->next = first;
first = p;
p = 0;
```