# ISO/IEC 14882:2017(E)

- end example|
9 When looking for the declaration of a name used in a template definition, the usual lookup rules (6.4.1, 6.4.2) are used for non-dependent names. The lookup of dependent names is postponed until the template parameters are known (17.6.2). [Example:

```
#include <iostream>
using namespace std;

template<class T> class Set {
    T p;
    int cnt;
public:
    Set();
    Set(const Set<T>& k);
    void print() {
        for (int i = 0; i<cnt; ++i)
            cout << p << "\n";
    }
};
```

in the example, the local variable i is declared in print. However, not every declaration can be found this way; the resolution of some names is postponed until the template-arguments are known. For example, even though the operator<< is known within the definition of print() and a declaration of it can be found in <iostream>, the actual declaration of operator<< needed to print p(i) cannot be known until what type T is (17.6.2). — end example

10 If a name does not depend on a template-argument (as defined in 17.6.2), a declaration (or set of declarations) is bound to the declaration (or declarations) at the point where the name appears in the template definition: the name is visible at the point of instantiation. This binding is not affected by declarations void f(char); [Example:

```
template<class T> void g(T t) {
    f(1);\        // f(char)
    f(T(1));      // dependent
    f(t);
    dd++;        // dependent; error: declaration for dd not found
}
```

```
enum E { e };
void f(E);
double dd;
void h() {
    g(e);          // will cause one call of f(char) followed by two calls of f(E)
    g(char*));     // will cause three calls of f(char)
}
```

- end example

11 [Note: For purposes of name lookup, default arguments and noexcept-specifiers of function templates and default arguments and noexcept-specifiers of member functions of class templates are considered definitions (17.5). end note]

©ISO/IEC 2017 – All rights reserved

376