# ISO/IEC 14882:2017(E)

makes a color type describing various colors, and declares col as an object of type, and cp as a pointer to an object of type. The possible values of an object of type color are red, yellow, green, blue; these values can be converted to the integral values 0, 1, 20, and 21. Enumerations are distinct types, objects of type color can be assigned only values of type color.

```
color c = 1;               // error: mismatch, no conversion from int to color
int i = yellow;             // OK: yellow converted to integral value 1, integral promotion
```

Note that this enum to int conversion is not provided for a scoped enumeration:

```
enum Col { red, yellow, green };
int x = Col::red;           // error: no Col to int conversion
if (y == Col) {              // error: no Col to bool conversion
// end enum
```

+   11 Each enum-name and each scoped enumerator is declared in the scope that immediately contains the enum-specifier. The scope rules define for all names in 6.3 and 6.4. | Example:
enum direction {left='l', right='r'};

```
void g() {
    direction d;           // OK
    d = left;               // OK
    d = direction::right;
}
```

```
void h(altitude high='h', low='l') {
    altitude a;
    a = high;               // error: high not in scope
    a = altitude::low;      // OK
}
```

> end An enumerator declared in the scope can be referred to using the class member access operators (::, (dot) and -> (arrow)), see 8.2.5. | Example:

```
struct X {
    enum direction {left='l', right='r'};
    int f(int i) return i=left ? 0 : i=right ? 2;
};
```

```
void g(X* p) {
    direction d;           // error: direction not in scope
    int i;
    i = p->left(left);      // error: left not in scope
    i = p->X(right);        // OK
    i = p->f(p->left);
    //...
}
```

+   12 If an enum-header has a nested-name-specifier, the enum-specifier shall refer to an enumeration was previously declared directly in the class or namespace, or in an element of the inline namespace scope (10.3.1) of namespace (i.e., not merely inherited or introduced by a using-declaration), and the enum-specifier shall appear in a namespace enclosing the previous declaration. In

§ 10.2                                                              ©ISO/IEC 2017 - All rights reserved 177