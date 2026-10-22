```
class C {};
    // definition (and declaration) of class C

void f(int p) {    // definition (and declaration) of function f()
    std::cout << p << '\n';
}

extern int v = 1;  // an initializer makes this a definition for v

int w;             // global variable declarations not preceded by
                   // extern are also definitions
```