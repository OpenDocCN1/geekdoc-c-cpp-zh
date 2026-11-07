**TABLE 18-2** Values of first, last, and mid and the Number of Comparisons for Search Item 34

| Iteration | first | last | mid | list[mid] | Number of comparisons |
|---|---|---|---|---|---|
| 1 | 0 | 11 | 5 | 39 | 2 |
| 2 | 0 | 4 | 2 | 19 | 2 |
| 3 | 3 | 4 | 3 | 25 | 2 |
| 4 | 4 | 4 | 4 | 34 | 1 (found is true) |

The item is found at location 4, and the total number of comparisons is 7.

Let us now search for item 22, as shown in Table 18-3.

**TABLE 18-3** Values of first, last, and mid and the Number of Comparisons for Search Item 22

| Iteration | first | last | mid | list[mid] | Number of comparisons |
|---|---|---|---|---|---|
| 1 | 0 | 11 | 5 | 39 | 2 |
| 2 | 0 | 4 | 2 | 19 | 2 |
| 3 | 3 | 4 | 3 | 25 | 2 |
| 4 | 3 | 2 | the loop stops (because first > last) | | |

This is an unsuccessful search. The total number of comparisons is 6.

Example 18-2 illustrates how to use the binary search algorithm in a program.

# EXAMPLE 18-2

```
```cpp
#include <iostream>
#include "searchSortAlgorithms.h"

using namespace std;

int main()
```
```