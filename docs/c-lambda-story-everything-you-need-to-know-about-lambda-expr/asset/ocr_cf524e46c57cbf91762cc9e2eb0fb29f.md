like constexpr or constval in C++17 and C++20.

# Attributes

The syntax for lambdas also allows using attributes introduced in the form of [[attr_name]]. However, if you apply an attribute to a lambda, then it applies to the type of the call operator and not to the operator itself. That's why currently (and even in C++20) there are no attributes that make sense to put on a lambda. Most compilers report an error. If we take a C++17 attribute and try to use it with the expression:

```
auto myLambda = [](int a) [[nodiscard]] { return a * a; };
```

Generates the following errors on Clang (see code @Sandbox):

error: 'nodiscard' attribute cannot be applied to types

# Compiler Expansion

As a summary, here's a basic example that shows how to write a lambda expression and pass it to std::for_each. For comparison, the code also illustrates the corresponding functor type:

First Lambda and a Corresponding Functor. Live code @Wandbox

```
#include <algorithm>
#include <iostream>
#include <vector>

int main() {
  struct {
    void operator()(int x) const {
      std::cout << x << '\n';
    } someInstance;

  const vector<int> v = { 1, 2, 3 };
  std::for_each(v.begin(), v.end(), someInstance());
  std::for_each(v.begin(), v.end(), [] (int x) {
    std::cout << x << '\n';
  });
\}
```

In the example, the compiler transforms...

```
[](int x) { std::cout << x << '\n'; }
```

...into an anonymous functor that in a simplified form can look as follows: