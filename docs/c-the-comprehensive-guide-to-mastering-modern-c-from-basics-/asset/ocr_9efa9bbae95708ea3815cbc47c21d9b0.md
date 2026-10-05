I declare v as a variant that can contain either a value of type int or one of type float. Then I assign v with 12 int, which I read and output with get<int>. This is followed by another assignment with a value, but this time a float. I also read and output this one. v has has contained first an int and then a float in succession.

You cannot request a type with get that variant does not know. get<double> does not compile.

At runtime, you will get an error if you query a valid type that variant does not currently contain. You will receive the bad_variant_access exception.

Without an exception, you check the state with holds_alternative<int>(w). Here you get a bool indicating whether w holds an int or not.

If you want to react to the content of variant, you can query which one is current with index. However, it is more elegant to use visit, to which you pass a visitor that can handle the different types.

```
// https://godbolt.org/z/G4zY5E6P
#include <variant>
#include <iostream>
using std::cout;
struct TypeGreeting {
    void operator()(int) const { cout << "Hello int"; }
    void operator()(float) const { cout << "Hello float"; }
};
int main() {
    std::variant<int, float> var;
    var = 12; // State int
    std::visit([](auto a) { cout << a; }, var); // generic lambda
    cout << std::endl;
    var = 3.456f; // State float
    std::visit(TypeGreeting{}, var); // Functor with overloadsn
```