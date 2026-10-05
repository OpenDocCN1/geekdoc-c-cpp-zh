# Modern C++: [[deprecated]] Attribute (C++14)

The [[deprecated]] keyword warns a user that an expression, function, class or feature can be used but its usage is discouraged. The syntax is:

```
[[deprecated]]
expression, function, class or enum that is deprecated
```

The compiler will emit a warning that the item is deprecated. An optional message can be attached by using the following syntax:

```
[[deprecated("message")]]
```

Examples:

```
// identifying the use of a deprecated function
[[deprecated("postgres sqlConnect function is obsolete")]]
int sqlConnect() {
```

```
// identifying the use of a deprecated class
#include <iostream>
using namespace std;

int main() {
class [[ deprecated("Foo is obsolete") ]] Foo {
public:
  Foo() { cout << "in constructor" << endl; }
  int x;
};
Foo foo;
}
```

```
// returns
warning: 'Foo' is deprecated: Foo is obsolete
```