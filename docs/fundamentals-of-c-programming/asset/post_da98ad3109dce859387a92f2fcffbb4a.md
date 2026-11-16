
std::cout << '\n';
std::cout << "-----------------------------------\n";
std::cout << "Partitioned sequence" << '\n';
std::partition(std::begin(words), std::end(words),
               [](const std::string& w) { return w.length() > 3; });
std::copy(std::begin(words), std::end(words), string_output);
std::cout << '\n';
}

### Listing 20.43 (testpartition.cpp) prints

```
Original sequence
81 80 2 63 13 25 12 7 8 16 84 91 56 91 56 7 59 94 18 68 68 71 78 66 60

Partitioned sequence
60 80 2 66 78 68 12 68 8 16 84 18 56 94 56 7 59 91 91 7 25 71 13 63 81
...............................................................

Original sequence
fred ella adam jo pat mel anna ed oscar will tom ingrid

Partitioned sequence
fred ella adam ingrid will oscar anna ed mel pat tom jo
```

Note that std::partition does not attempt to preserve the original relative order of elements within a partition. Also, std::partition does not make any new string objects; it simply moves existing string objects around within the container. This makes std::partition as efficient for strings as for simple numbers.

## std::merge.

Suppose we have two sorted sequences, and we wish to combine them into one large sorted sequence. One way to do this would be to copy the two sequences into a larger container and then sort the container, as in the following:

```
// v1 and v2 are two sorted vectors containing integers
std::vector<int> merged(v1.size() + v2.size());
auto last = std::copy(v1.begin(), v1.end(), merged.begin());
std::copy(v2.begin(), v2.end(), last);
std::sort(merged.begin(), merged.end());
```

This process will produce the correct result, but it is not efficient. Consider how you might merge two stacks of sorted cards to produce a larger stack of sorted cards. Would you place one stack of the cards on top of the other stack of cards and then re-sort this new, larger stack of cards? Sorting is a time-consuming process. You must look at each card and search for the proper place to relocate it within the deck. This repeated searching is what slows down the process. It is much faster to look at the top cards on both stacks, choose the smaller of the two top cards, and place it face down on the new stack. Continue this process, always selecting the smaller top card and placing it face down on the new stack. When both of the original two stacks are empty, turn the newly formed stack over (so its cards will be facing up), and the resulting stack will contain all of the cards in sorted order. This is much faster because you never have to search for where to place a card—you simply pick the smaller of two visible cards and place it on the new stack.

The implementation of std::sort in the STL is a good one, but even with the best implementation, sorting in general is time consuming. Since merging two sorted sequences into a new sorted sequence is a common activity, the STL provides the std::merge function. The std::merge function merges two ordered containers into a third container. The resulting container will be ordered. Listing 20.44 (testmerge.cpp) provides an example of the use of std::merge.

### Listing 20.44: testmerge.cpp

```
#include <iostream>
#include <vector>
#include <algorithm>
#include <iterator>
#include <random>

// Uniform pseudorandom number generator from an earlier chapter
// include "uniformrandom.h"

int main() {
    std::vector<int> nums1(15),
                     nums2(13);

    UniformRandomGenerator gen1(0, 40),
                               gen2(0, 40);

    auto output = std::ostream_iterator<int>(std::cout, " ");

    // Populate the vectors with pseudorandom
    // integers in the range 0, 1, ..., 50
    std::generate(std::begin(nums1), std::end(nums1), gen1);
    std::generate(std::begin(nums2), std::end(nums2), gen2);

    std::cout << "Original sequences\n";
    std::copy(std::begin(nums1), std::end(nums1), output);
    std::cout << "\n";
    std::copy(std::begin(nums2), std::end(nums2), output);
    std::cout << "\n------------------\n";

    std::sort(std::begin(nums1), std::end(nums1));
    std::sort(std::begin(nums2), std::end(nums2));

    std::cout << "Sorted sequences\n";
    std::copy(std::begin(nums1), std::end(nums1), output);
    std::cout << "\n";
    std::copy(std::begin(nums2), std::end(nums2), output);
    std::cout << "\n------------------\n";

    // Merge the sequences
    std::vector<int> merged(nums1.size() + nums2.size());
    std::merge(std::begin(nums1), std::end(nums1),
               std::begin(nums2), std::end(nums2),
               std::begin(merged));

    std::cout << "Merged sequence\n";
    std::copy(std::begin(merged), std::end(merged), output);
    std::cout << "\n";
}
```

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

As previously mentioned, merging two containers using std::merge, as in the following code:

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

### Listing 20.45: comparemerges.cpp

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
    clock_t start = clock();
    std::vector<int> result(v1.size() + v2.size());
    std::merge(std::begin(v1), std::end(v1),
               std::begin(v2), std::end(v2),
               std::begin(result));
    clock_t stop = clock();
    std::cout << "Merge 1 elapsed time: "
              << static_cast<double>(stop - start) / CLOCKS_PER_SEC
              << " sec\n";
    return result;
}

// The vectors v1 and v2 must be in sorted order
std::vector<int> merge2(const std::vector<int>& v1,
                        const std::vector<int>& v2) {
    clock_t start = clock();
    std::vector<int> result(v1.size() + v2.size());
    auto last = std::copy(std::begin(v1), std::end(v1),
                          std::begin(result));
    std::copy(std::begin(v2), std::end(v2), last);
    std::sort(std::begin(result), std::end(result));
    clock_t stop = clock();
    std::cout << "Merge 2 elapsed time: "
              << static_cast<double>(stop - start) / CLOCKS_PER_SEC
              << " sec\n";
    return result;
}

int main() {
    const int SIZE = 10'000'000;
    std::vector<int> nums1(SIZE), nums2(SIZE);

    UniformRandomGenerator gen1(0, SIZE), gen2(0, SIZE);

    // Populate the vectors with pseudorandom
    // integers in the range 0, 1, ..., 50
    std::generate(std::begin(nums1), std::end(nums1), gen1);
    std::generate(std::begin(nums2), std::end(nums2), gen2);

    //std::cout << "Original sequences\n";
    //std::cout << "nums1\n";
    //std::cout << "nums2\n";
    //std::cout << "nums2\n";

    std::sort(std::begin(nums1), std::end(nums1));
    std::sort(std::begin(nums2), std::end(nums2));

    //std::cout << "Sorted sequences\n";
    //std::cout << "nums1\n";
    //std::cout << "nums2\n";
    //std::cout << "nums2\n";

    std::cout << "Merging . . " << '\n';
}
