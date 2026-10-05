# Modern C++: Structured Bindings (C++17)

Structured bindings assign values to scalar variables from the public data members of an object such as a struct, class, array or a tuple object.

The syntax for a structured binding is:

```
auto [myvar1, myvar2, myvar3] = some_object;
```

In the example below, we bind the elements of an array to three scalar variables:

```
#include <iostream>
int main()
{
    int arr[] = { 1, 2, 3 };
    auto [foo1, foo2, foo3] = arr;
    std::cout << foo1 << " " << foo2 << " " << foo3 << std::endl;

    return 0;
}
// output
1 2 3
```

In the following example, we bind three scalar variables to the members of a struct:

```
#include <iostream>
#include <string>
struct
{
    int x = 9;
    std::string s = "hello world";
    double y = 5.37;
} foo;
int main()
{
    auto [bar1, bar2, bar3] = foo;
    std::cout << bar1 << " " << bar2 << " " << bar3 << std::endl;
```