![](bbox=[0.16, 0.08, 0.8, 0.46])

# Figure 4-3: Appending vector entries

The method `resize(n)` shrinks or expands the vector to size `n`. New entries are default-constructed (or set to `0` for built-in types). Shrinking vectors with `resize` doesn't release memory. This can be done in C++11 with `shrink_to_fit` which reduces the capacity to the actual vector size.

=> c++11/vector_usage.cpp

C++11 The following simple program illustrates how a `vector` is set up and modified with C++11 features:

Click here to view code image

```
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main ()
{
    using namespace std;
    vector<int> v = {3, 4, 7, 9};
```
```