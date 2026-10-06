# ISO/IEC 14882:2017(E)

9 A lambda-expression appearing in a default argument shall not implicitly or explicitly capture entity.
[Example]:

```
void f2() {
  int i = 1;
  void g1(int = ([=](){ return 1; })); // ill-formed
  void g2(int = ([&](){ return 0; })); // ill-formed
  void g3(int = ([*](){ return 1; })); // ill-formed
  void g4(int = ([=](){ return 0; })); // OK
  void g5(int = ([](){ return sizeof(i); })); // OK

// end example
```

10 An entity is captured by a capture, and the captured entity is not *this, or

+   (10.1) it is implicitly captured, the capture-default =
(10.2) it is explicitly captured by a capture that is not of this this, & identifier, or identifier initializer.

For each entity captured by copy, an unnamed non-static data member is declared in the closure type. The declaration of these members is unspecified. The type of such member is the referenced type if the entity is a reference to an object, an i reference to the referenced function if the entity is a reference to a function, or the type of the corresponding captured entity otherwise. A member of anonymous entity shall be captured by copy.

11 Every id-expression within the body of a lambda-expression is an odr-expression (6.2) of an entity captured by copy is transformed into an access to the corresponding unnamed data member of the closure type. Note: An id-expression that is captured by copy, each odr-use of this is transformed into a pointer to the corresponding unnamed data member of the closure type. Furthermore, such id-expression does not refer to the original entity, nor to the member of the closure type. Note: If *this is captured by copy, each odr-use of this is transformed into a pointer to the corresponding unnamed data member of the closure type. Note: The closure ensures that the reference is bound by reference references to the entity to which it is captured. Note: An id-expression within the compound-statement of a lambda-expression that is an odr-use of a reference to the entity to which the capture is bound and not to the captured reference. Note: The validity of such captures is determined by the lifetime of the reference refers, not by the lifetime of the reference itself. end note) [Example]:

```
void f(const int*) {
void g() {
  const int N = 10;
  {} 
  int arr[N]; // OK: not an odr-use, refers to automatic variable
  f(arr); // OK: causes N to be captured; & points to
 corresponding member of the closure type
}
}
auto h(int k) {
  return r[k]; // After valid h returns the lifetime of the
 object to which r is bound has not ended
}

// end example
```