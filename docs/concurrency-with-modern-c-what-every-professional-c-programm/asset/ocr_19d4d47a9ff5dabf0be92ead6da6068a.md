# The new algorithms

| Algorithm | Description |
|---|---|
| `std::exclusive_scan` | Applies from the left a binary callable up to the ith (exclusive) element of the range and writes the result to an output range. The left argument of the callable is the previous result. Stores intermediate results. If the binary callable is non-associative the result is non-deterministic. Similar to `std::partial_sum`⁶ |
| `std::inclusive_scan` | Applies from the left a binary callable up to the ith (inclusive) element of the range and writes the result to an output range. The left argument of the callable is the previous result. Stores intermediate results. If the binary callable is non-associative the result is non-deterministic. Similar to `std::partial_sum`⁶ |
| `std::transform_exclusive_scan` | First applies a unary callable to the range and then applies `std::exclusive_scan`. If the binary callable is non-associative the result is non-deterministic. |
| `std::transform_inclusive_scan` | First applies a unary callable to the range and then applies `std::inclusive_scan`. If the binary callable is non-associative the result is non-deterministic. |
| `std::reduce` | Applies from the left a binary callable to the range. If the binary callable is non-associative or non-commutative the result is non-deterministic. Similar to `std::accumulate`⁷ |
| `std::transform_reduce` | Applies a unary callable to one or a binary callable to two ranges and then `std::reduce` to the resulting range. If the binary callables are non-associative or non-commutative the result is non-deterministic. |

Admittedly this description is not easy to digest, but if you already know `std::accumulate` and `std::partial_sum`, the reduce and scan variations should be quite familiar. reduce is the parallel pendant to accumulate and scan the parallel pendant to partial_sum. The parallel execution is the reason that `std::reduce` needs an associative and commutative callable. The corresponding statement holds for the scan variations in contrary to the partial_sum variations.

First, I present an exhaustive example of the algorithms and then write about these functions’ functional heritage. In my example, I ignore the new `std::for_each` algorithm. In contrast to the C++98 variant that returns a unary function, the additional C++17 variant returns nothing. While `std::accumulate` processes its elements from left to the right, `std::reduce` does it in an arbitrary order. Let me start with a small code snippet using `std::accumulate` and `std::reduce`. The callable is the lambda function `[](int a, int b){ return a * b; }`.

⁶ http://en.cppreference.com/w/cpp/algorithm/partial_sum
⁷ http://en.cppreference.com/w/cpp/algorithm/accumulate