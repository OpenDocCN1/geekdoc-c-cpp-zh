consideration. To see this, we will investigate the operation of the following summation algorithms:

+   - The simple multiply-and-add method
+   - A method that computes the element-wise products, sorts them, and does a summation
+   - The Kahan summation method, which applies a correction factor on the underflow bits

Each of these algorithms is implemented in a different function. We have gathered all of them, as well as other definitions and test functions, in the `InnerProducts` namespace, which begins on line [8] in Listing 7.14. Some useful aliases are grouped starting on line [11]. Similarly, objects from the standard library are listed starting on line [15].

The function `InnerProduct_StdAlg` starts on line [21]. The only call it makes on line [24] is to `std::inner_product`, which computes the inner product of two vectors v and w, exactly as in Eq. (7.42). For this purpose, the full range of v needs to be provided in its two first arguments. The third is the beginning of w. But the last is an initial start value for the sum in Eq. (7.42). We must be careful to choose its correct type, which agrees with the type of elements in v and w. Otherwise, nasty errors can arise. Alas, we will see that in some cases, `std::inner_product` can be highly inaccurate due to floating-point errors.

```
```cpp
#include <vector>
#include <iostream>
#include <iomanip>
#include <random>
#include <numeric>      // for inner product

namespace InnerProducts
{
    using DVec = std::vector<double>;
    using DT = DVec::value_type;
    using ST = DVec::size_type;

    using std::inner_product;
    using std::transform;
    using std::accumulate;
    using std::sort;
    using std::cout; using std::endl;

auto InnerProduct_StdAlg( const DVec & v, const DVec & w )
{
    // The last argument is an initial value
    return inner_product( v.begin(), v.end(), w.begin(), DT() );
}
```
```

The situation can be remedied by summing onto an output sum that has higher precision than the summands. However, such an approach has a number of limitations. First, we need to have a FP representation with higher precision. Using many libraries, such as GMP⁶ and tmmath,⁷ can be cumbersome on some platforms and almost always incurs a runtime penalty.