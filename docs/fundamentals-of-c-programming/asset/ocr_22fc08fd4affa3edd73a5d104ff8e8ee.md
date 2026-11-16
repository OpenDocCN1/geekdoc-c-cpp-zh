```
auto m1 = merge1(nums1, nums2);
//std::cout << "Merged sequence\n";
//std::cout << m1 << '\n';

auto m2 = merge2(nums1, nums2);
//std::cout << "Merged sequence\n";
//std::cout << m2 << '\n';

std::cout << std::boolalpha << (m1 == m2) << '\n';
}
```

Listing 20.45 (comparemerges.cpp) merges two vectors of size 10,000,000. The program's output show the dramatic difference in execution times:

```
Merging ...
Merge 1 elapsed time: 0.182
Merge 2 elapsed time: 3.859
true
```

This result is representative of the speedup—the version that uses std::merge is over 20 times faster than the copy-then-sort version. The disparity of the running times slowly grows as the size of the sequences to merge increases.

**std::remove.** Suppose we wish to remove all the elements from a container that equal a particular value. The STL provides a function named std::remove that sounds promising, but by itself it does not achieve the result we generally desire. Consider Listing 20.46 (testsimpleremove.cpp) which offers a simple experiment with the std::remove function.

# Listing 20.46: testsimpleremove.cpp

```
#include <iostream>
#include <vector>
#include <algorithm>
#include "vectorprint.h"

int main() {
  std::vector<int> nums { 4, 7, 2, 3, 7, 9, 0, 1, 8 };
  std::cout << "Original vector: " << nums << '\n';

  // Remove 7
  std::remove(std::begin(nums), std::end(nums), 7);
  std::cout << "Vector with 7 removed: " << nums << '\n';
}
```

The compiler issues a warning about discarding a return value of a function with a nodiscard attribute, but it reports no errors. Executing the program produces the following output:

```
Original vector: {4, 7, 2, 3, 7, 9, 0, 1, 8}
Vector with 7 removed: {4, 2, 3, 9, 0, 1, 8, 1, 8}
```

The element 7 definitely is gone from the resulting vector, but the vector still contains the original number of elements. The std::remove function copied elements that follow each 7 forward to overwrite the occurrences of 7. It appears that the implementation of std::remove is incomplete and that the author of the function forgot to write the code that removes the last two elements from the resulting vector!