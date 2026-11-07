# **push_heap Algorithm**

Line 40 uses the `push_heap` algorithm to add a new value into a heap. We take one element of an array init at a time, append it to the end of vector v and perform the push_heap operation. If the appended element is the only element in the vector, the vector is already a heap. Otherwise, push_heap rearranges the vector elements into a heap. Each time push_heap is called, it assumes that the last element currently in the vector (i.e., the one that's appended before the push_heap call) is the element being added to the heap and that all other elements in the vector are already arranged as a heap. The two iterator arguments to push_heap must be *random-access iterators*. A second version of this algorithm takes as a third argument a *binary predicate function* for comparing values.

# **pop_heap Algorithm**

Line 51 uses the `pop_heap` to remove the *top* heap element. This algorithm assumes that the elements in the range specified by its two *random-access iterator* arguments are already a heap. Repeatedly removing the *top* heap element results in a sorted sequence of values. Algorithm `pop_heap` swaps the first heap element (v.begin()) with the last heap element (the element before v.end() - 1), then ensures that the elements up to, but not including, the last element still form a heap. Notice in the output that, after the pop_heap operations, the vector is *sorted* in ascending order. A second version of this algorithm takes as a third argument a *binary predicate function* for comparing values.

# **C++11: is_heap and is_heap_until Algorithms**

In addition to the make_heap, sort_heap, push_heap and pop_heap algorithms presented in Fig. 16.12, C++11 now includes the new algorithms is_heap and is_heap_until. The `is_heap` algorithm returns true if the elements in the specified range represent a heap. A second version of this algorithm takes as a third argument a *binary predicate function* for comparing values.

The `is_heap_until` algorithm checks the specified range of values and returns an iterator pointing to the last item in the range for which the elements up to, but not including, that iterator represent a heap.

# 16.3.13 min, max, minmax and minmax_element

Figure 16.13 demonstrates algorithms min, max, minmax and minmax_element.

```
```cpp
// Fig. 16.13: fig16_13.cpp
// Algorithms min, max, minmax and minmax_element.
#include <iostream>
#include <array>
#include <algorithm>
using namespace std;

int main()
{
    cout << "The minimum of 12 and 7 is: " << min(12, 7);
    cout << "\nThe maximum of 12 and 7 is: " << max(12, 7);
    cout << "\nThe minimum of 'G' and 'Z' is: " << min('G', 'Z');
```

```

**Fig. 16.13** | Algorithms min, max, minmax and minmax_element. (Part 1 of 2.)