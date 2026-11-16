One run of Listing 20.44 (testmerge.cpp) prints the following:

```
Original sequences
8 26 8 17 26 23 31 7 16 30 5 21 37 20 4
-------------------------------------------
29 0 22 32 18 4 4 36 26 38 21 14 34 32
-------------------------------------------
Sorted sequences
4 5 7 8 8 16 17 20 21 23 26 26 30 31 37
-------------------------------------------
0 4 4 14 18 21 22 26 29 32 32 34 36 38
-------------------------------------------
Merged sequence
0 4 4 5 7 8 8 14 16 17 18 20 21 21 22 23 26 26 26 29 30 31 32 32 34 36 37 38
```

As you can see, the std::merge function would be useful if you have two ordered containers that you wish to combine, and you want the elements in the resulting container to be ordered.

As previously mentioned, merging two containers using std::merge, as in the following code: following code:

```
std::vector<int> merged(nums1.size() + nums2.size());
std::merge(std::begin(nums1), std::end(nums1),
           std::begin(nums2), std::end(nums2),
           std::begin(merged));
```

is much more computationally efficient than copying and then sorting, as in the following code:

```
std::vector<int> merged(nums1.size() + nums2.size());
auto last = std::copy(std::begin(nums1), std::end(nums1),
                      std::begin(merged));
std::copy(std::begin(nums2), std::end(nums2), last);
std::sort(std::begin(merged), std::end(merged));
```

Listing 20.45 (comparemerges.cpp) compares the two different approaches to merging two sorted sequences.

# Listing 20.45: comparemerges.cpp

```
#include <iostream>
#include <vector>
#include <algorithm>
#include <iterator>
#include <random>
#include <ctime>

#include "vectorprint.h"
// Uniform pseudorandom number generator from an earlier chapter
#include "uniformrandom.h"

// The vectors v1 and v2 must be in sorted order
std::vector<int> merge1(const std::vector<int>& v1,
                        const std::vector<int>& v2) {
```