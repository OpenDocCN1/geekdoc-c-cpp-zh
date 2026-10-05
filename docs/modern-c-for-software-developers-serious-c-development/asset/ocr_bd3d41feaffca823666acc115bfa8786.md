# The Scope Resolution Operator

The :: scope resolution operator associates a member with a class name. This tells the compiler which class the member belongs to. The scope resolution operator also has another related use: it can allow access to a name within some scope. This allows access to a name in some scope that is identical to a local declaration with the name.

The following example shows how this works:

```
int i;      // global variable i
void f() {
    int i;      // local variable i
    i = 10;     // uses local i
}

void g() {
    int i;      // local variable i
    ::i = 10;    // refers to the global variable i
}
```

# Class Function Implementations

Consider the following class specification:

```
#include <iostream>
#include <cstring>

using namespace std;

class Foo {
public:
    void buildstr(char *s);
    void showstr();

private:
```