# Reference to Member Variable in Lambda Capture

Here’s an example program that demonstrates capturing a member variable of a class in a lambda function through a reference:

```
#include <iostream>

class MyClass {
public:
    MyClass(int value) : myMember(value) {}

    void doOperation() {
        int multiplier = 2;
        auto lambda = [this, &multiplier]() {
            myMember *= multiplier;
            std::cout << "Inside lambda: myMember = " << myMember << std::endl;
        };

        lambda();
        std::cout << "After lambda: myMember = " << myMember << std::endl;
    }
}
```