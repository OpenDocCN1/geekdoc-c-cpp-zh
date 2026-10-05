# C++ Standard Library: std::optional

Consider a function that returns the index at which the number zero is found in some text. It is perfectly acceptable and not an error if zero does not exist in the text. std::optional is designed to handle these types of situations. The template std::optional is declared as follows:

```
#include <optional>
std::optional<class T> var;
```

std::optional<class T> consists of all possible values of type T and the value std::nullopt. std::nullopt represents no value or nothing. std::nullopt semantically represents the absence of a value.

The following example shows a typical use of std::optional:

```
#include <iostream>
#include <optional>

using namespace std;

optional<unsigned int> evenNumber(unsigned int num) {
    if (num == 0)
        return num;

    return nullopt;
}

int main() {
    std::optional<unsigned> opt = evenNumber(5);

    if (opt.has_value()) {
        cout << "The number is "
             << opt.value()
             << "\n";
    } else
        cout << "no value returned";

}
```