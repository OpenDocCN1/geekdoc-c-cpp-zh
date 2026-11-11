```
```cpp
}
```
```

The program executes two promises in their threads. The resulting futures are fire and forget futures. These futures block in their destructors until the associated promise is done. The result is that the promises are executed in the sequence which you find in the source code. The execution sequence is independent of the execution time. This is what you see in the output of the program.

![](bbox=[0.266, 0.309, 0.729, 0.424])

Fire and forget futures

std::async is a convenient mechanism used to distribute a bigger compute job on more shoulders.

# ### 3.9.2.3 Concurrent Calculation

The calculation of the scalar product can be spread across four asynchronous function calls.

**Dot product with four futures**

```
```cpp
// dotProductAsync.cpp

#include <iostream>
#include <future>
#include <random>
#include <vector>
#include <numeric>

using namespace std;

static const int NUM = 10000000;

long long getDotProduct(vector<int>& v, vector<int>& w) {

    auto vSize = v.size();

    auto future1 = async([&] {
```
```