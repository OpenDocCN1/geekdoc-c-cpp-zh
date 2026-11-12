# Algorithm 63. Kadane’s 1D Algorithm

```
```text
1: function KADANE1D(start, end)
2:     max_so_far ← 0
3:     max_ending_here ← 0
4:     while start ≠ end do
5:         max_ending_here ← max(max_ending_here + *start, 0)
6:         max_so_far ← max(max_so_far, max_ending_here)
7:         start ← start + 1
8:     end while
9:     return max_so_far
10: end function
```
```

# C++11 Implementation

Program 4.4: Implementing Kadane’s Algorithm

```
```cpp
#include <algorithm>

template <typename ForwardIterator>
typename std::iterator_traits<
    ForwardIterator>::value_type
kadane1d(ForwardIterator start,
         ForwardIterator end)
{
    typedef typename std::iterator_traits<
        ForwardIterator
    >::value_type value_type;

    value_type max_so_far = 0,
               max_ending_here = 0;

    while (start != end)
    {
        max_ending_here =
            std::max(max_ending_here + *start++,
                     0);
        max_so_far =
            std::max(max_so_far, max_ending_here);
    }
    return max_so_far;
}
```
```

# Usage

Program 4.5: Implementing Kadane’s Algorithm

```
```cpp
#include <iostream>
#include <array>
#include <vector>
#include <forward_list>
#include "kadane1d.hpp"
```
```