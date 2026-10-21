Another application of the new expression evaluation order is the function that inserts a space before passed arguments.

# Backward Incompatibilities

The new guaranteed evaluation order might impact the output of existing programs. This is not just theory. Consider, for example, the following program:

lang/evalexcept.cpp

```
#include <iostream>
#include <vector>

void print10elems(const std::vector<int>& v) {
    for (int i=0; i<10; ++i) {
        std::cout << "value: " << v.at(i) << '\n';
    }
}

int main()
{
    try {
        std::vector<int> vec{7, 14, 21, 28};
        print10elems(vec);
    }
    catch (const std::exception& e) {    // handle standard exception
        std::cerr << "EXCEPTION: " << e.what() << '\n';
    }
    catch (...) {                        // handle any other exception
        std::cerr << "EXCEPTION of unknown type\n";
    }
}
```

Because the vector<> in this program has only four elements, the program throws an exception in the loop in print10elems() when calling at() as part of an output statement for an invalid index:

```
std::cout << "value: " << v.at(i) << "\n";
```

Before C++17, the output could be:

```
value: 7
value: 14
value: 21
value: 28
EXCEPTION: ...
```