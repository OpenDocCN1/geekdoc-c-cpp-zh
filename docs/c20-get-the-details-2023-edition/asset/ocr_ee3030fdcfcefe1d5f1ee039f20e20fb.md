# Using `std::remove_if` to remove elements from a container

```
```cpp
// removeElements.cpp

#include <algorithm>
#include <iostream>
#include <vector>

int main() {

    std::cout << '\n';

    std::vector myVec{-2, 3, -5, 10, 3, 0, -5};

    for (auto ele: myVec) std::cout << ele << " ";
    std::cout << "\n\n";

    std::remove_if(myVec.begin(), myVec.end(), [](int ele){ return ele < 0; });
    for (auto ele: myVec) std::cout << ele << " ";

    std::cout << "\n\n";
}
```
```

The program removeElements.cpp removes all elements from the std::vector that are less than zero. Easy, right? Maybe not; now, you fall into the trap that is well-known to many seasoned C++ programmer.

![](bbox=[0.296, 0.609, 0.704, 0.78])

Using `std::remove_if` to remove elements from a container

`std::remove_if` (lines 16) does not remove anything. The std::vector still has the same number of arguments. Both algorithms return the new logical end of the modified container.

To modify a container, you have to apply the new logical end to the container.