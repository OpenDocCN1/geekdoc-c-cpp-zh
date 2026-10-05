conversion from a const& to a & is not permitted. This is not like name1, where a const& string was converted into a string by copying it.

+   - string with auto name4 = w.getName();
The compiler sets auto to the type string. Thus, the type of the variable is string.

+   - const string& with const auto name5 = w.getName();
Again, the compiler substitutes string for auto. The overall type is then const string&.

When a class returns a reference, it is quite common to also mark it with const. You often do not want external changes to values that reside within the class. Therefore, you first choose to return by value, and if that is inappropriate, by reference. Whether it is const or not depends on the intended use.

For reference returns, both are conceivable. Sometimes you want the value to be changeable from outside, sometimes not.

```
// https://godbolt.org/9MTj3rP5d
#include <string>
#include <iostream>
using std::string; using std::cout;

class Widget {
    string name_();
public:
    const string& readName() const; // const&-return, const-
    method;
    string& getName(); // &-return
};
```

```
const string& Widget::readName() const { return name_; }
string& Widget::getName() { return name_; }
```

```
int main() {
    Widget w{};
```