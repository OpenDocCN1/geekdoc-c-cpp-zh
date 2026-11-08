# ## Implicitly capturing the this pointer by copy

```
```cpp
// lambdaCaptureThis.cpp

#include <iostream>
#include <string>

struct LambdaFactory {
    auto foo() const {
        return [=] { std::cout << ' ' << '\n'; };
    }
    std::string s = "LambdaFactory";
    ~LambdaFactory() {
        std::cout << "Goodbye" << '\n';
    }
};

auto makeLambda() {
    LambdaFactory lambdaFactory;

    return lambdaFactory.foo();
}

int main() {

    std::cout << '\n';

    auto lam = makeLambda();
    lam();

    std::cout << '\n';


}
```
```

The compilation of the program works as expected, but this does not hold for the execution of the program.