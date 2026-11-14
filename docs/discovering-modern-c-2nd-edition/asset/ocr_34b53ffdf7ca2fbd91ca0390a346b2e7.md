convinced that modules with homonymous namespaces are much easier to use. Finally, we `export` the function `is_prime`. Everything else that we might implement in our module won’t be seen outside; only what we `export` can be used. This means that we have the full control of what is seen outside the module, in contrast to header files due to their textual inclusion. Instead a module file is translated by the compiler and the result is accordingly a pre-compiled module file.

=> modules/math.cpp

The implementation of this function resides in a regular source file:

Click here to view code image

```
module math;

#include <cmath>

using namespace std;

namespace math {

long max_check(long i) { return std::sqrt(i) + 1; }

bool is_prime(long i)
{
    if (i == 1)
        return false;
    if (i % 2 == 0)
        return i == 2;
    for (long j = 3; j < max_check(i); j+= 2)
        if (i % j == 0)
            return false;
    return true;
}

} // namespace math
```

The only specialty here is the module declaration at the beginning. When we compile this file, the compiler needs the pre-compiled module file.

=> module/math_app.cpp

In our application, we import the module:

Click here to view code image