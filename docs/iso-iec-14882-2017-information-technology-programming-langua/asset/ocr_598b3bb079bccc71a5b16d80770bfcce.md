# ISO/IEC 14882:2017(E)

3 A bit-field shall not be a static member. A bit-field shall have integral or enumeration type (6.9.1). A bool value can successfully be stored in a bit-field of nonzero size. The address-of operator & shall not be applied to a bit-field, so there are no pointers to bit-fields. A non-const reference shall not be bound to a bit-field (11.6.3). [Note: If the initializer for a reference of const & is a reference to a bit-field, the reference is bound to a temporary object to hold the value of the bit-field; the reference is not bound to the bit-field. See 11.6.3.] — end note

4 If the value true or false is stored in a bit-field of bool size (including one bit bit-field), the original value and the bit-field shall compare equal. If the value of enumeration is stored into a bit-field of the same enumeration type and the number of bits in the bit-field is large enough to hold all values (10.2), the original enumeration value and the value of the bit-field shall compare equal. [Example]:

```
enum B {FALSE=0, TRUE=1};
struct A {
  bool b:1;
  int a;
  void f() {
    a.b = TRUE;
    if (a.b == TRUE)
      /* ... */
  }
};
```

end example

# 12.2.5 Nested class declarations [class.next]

1 A class can be declared within another class. A class declared within another is called a nested class. The name of the nested class is local to its enclosing class. [Note: See 8.1] for restrictions on the use of non-static data members and non-static member functions. — end note

Example:

```
int x;
int y;

struct enclose {
  int x;
  static int s;

  struct inner {
    void f(int i) {
      int a = sizeof(x);\ // OK: operand of sizeof is an unvaluated operand
      x = i; // error: assign to enclose::x
      s = i; // OK: assign to enclose::s
      y = i; // OK: assign to global x
      // OK: assign to global y
    }

  void g(enclose* p, int i) {
    p->x = i; // OK: assign to enclose::x
  }
};

inner* p = 0; // error: inner not in scope
```