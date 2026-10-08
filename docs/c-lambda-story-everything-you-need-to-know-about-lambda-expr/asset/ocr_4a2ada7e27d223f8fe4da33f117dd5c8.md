In C++20 there's also one more execution policy: unsequenced_policy along with the global instance std::execution::unseq. It's used to enable vectorisered execution on a single thread.

# While we can easily enable parallel sorting, we can also quickly write some bad code:

Copying into vector and dangerous behaviour.

```
#include <iostream>
#include <vector>
#include <numeric>
#include <execution>

int main () {
    std::vector<int> vec(1000);
    std::iota(vec.begin(), vec.end(), 0);
    std::vector<int> output;
    std::for_each(std::execution::par, vec.begin(), vec.end(),
        [&](int &elem) {
            if (elem % 2 == 0) {
                output.push_back(elem);
            }
        });

    for (const auto & elem) cout << elem << ", ";
}
}
```

> The code above doesn't contain any "Live Code" link as it requires a compiler with the parallel algorithm support. This is possible in MSVC (starting with VS 2017) but doesn't work well with any online compiler. You can take the code and play inside Visual Studio.

Do you see all the issues here?

By passing a lambda to std::for_each we need to remember that the execution doesn't happen on a single thread and locally. Several threads might be used here, for example, using a thread pool solution. That's why accessing a shared output vector is not the best idea. Not only can you insert elements in a wrong order, but it can crash if several threads attempt to change the vector at the same time.