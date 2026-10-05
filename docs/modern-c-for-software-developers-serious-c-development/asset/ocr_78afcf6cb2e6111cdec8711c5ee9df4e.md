# Modern C++: Initializers In Range-Based Loops (C++20)

C++20 permits initializers to be used in range-based loops:

```
#include <iostream>
#include <vector>

using namespace std;

int main() {
    for (vector<int> vec {1, 2, 3}; auto v : vec) {
        cout << v << " ";
    }

    // output
1 2 3
```