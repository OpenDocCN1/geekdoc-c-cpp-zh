An independent reference variable must be initialized when it is declared.

# Dangling References

A dangling reference refers to a reference variable that points to a value that does not exist or does not have an addressable memory location. In the example below, the function returns a reference that points to a local value on the stack:

```
```
#include <iostream>
int& foo() {
    int x = 5;
    return x;
}
int main() {
    int& ret = foo();
    std::cout << ret << std::endl;
}
//n error: reference to local variable x returned.
```
```

This program will not compile. The return value exists on the stack and will cease to exist after the function returns.

# Returning A Const Reference From A Class Member Function

Consider the following program:

```
```
#include <string>
#include <iostream>
class Dog {
public:
    std::string name;
    Dog(std::string nm) { name = nm; }
    const std::string& get_name() { return name; }
};
```
```