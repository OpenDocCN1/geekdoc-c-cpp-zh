(line 30) behaves accordingly. `dynamSpan` models the unique use case of a constant range of modifiable elements.

![](bbox=[0.224, 0.159, 0.777, 0.377])

*(Constant/modifiable) ranges of (constant/modifiable) elements*

Finally, I want to mention two dangers you should know when using `std::span`.

# ### 5.2.7 Dangers of `std::span`

The typical issues of `std::span` are twofold. First, a `std::span` should not act on a temporary and second, the size of the underlying contiguous range of a `std::span` should not be modified.

# #### 5.2.7.1 A `std::span` on a Temporary

A `std::span` is never an owner. Therefore, a `std::span` does not extend the lifetime of its data. Consequently, a `std::span` should only operate on an lvalue. Using a `std::span` on a temporary is undefined behavior.

**A `std::span` on temporary data**

```
```cpp
// temporarySpan.cpp

#include <iostream>
#include <span>
#include <vector>

std::vector<int> getVector() {
    return {1, 2, 3, 4, 5};
}

int main() {

    std::cout << '\n';
```
```