+   - Functions and methods
You already know them: you define a header with return type, function name, call parameters, and the function body.

+   - Functors or function objects
A functor is a class that defines the operator().
Instances of this class then behave like a function.

+   - Anonymous functions or lambdas
If you want to pass an operation to an algorithm—for example, "How do I compare for sorting?”—you can pass the function body (the "How") directly as a parameter without defining a function beforehand. This is why it is called an *anonymous function or*, in computer science jargon, a *lambda expression*.

Instances of a class with an operator() method behave like functions. You can call them as in the following listing.

```
// https://godbolt.org/z/xvfvG8hrd
#include <iostream> // cout
using std::;
class Increment {
    int amount_;
public:
    explicit Increment(int amount) : amount_{amount} {}
    int operator(int value) const { // makes instances callable
        return value + amount_;
    }
    void clear() {
        amount_ = 0;
    }
};
int main() {
    Increment PlusFour(4); // create instance
    Increment PlusEleven(1); // another instance
    cout << PlusFour(8) << "\n"; // Output: 12
    int result = 2 * PlusEleven(5) - 7; // result is 25
    cout << PlusEleven(result/5) << "\n"; // Output: 16
```