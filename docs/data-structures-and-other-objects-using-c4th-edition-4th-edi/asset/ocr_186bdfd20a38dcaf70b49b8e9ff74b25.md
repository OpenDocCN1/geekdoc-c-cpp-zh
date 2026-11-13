# FIGURE 3.6 Implementation File for the Bag Class

# An Implementation File

```
```cpp
// FILE: bag1.cxx
// CLASS IMPLEMENTED: bag (see bag1.h for documentation)
// INVARIANT for the bag class:
//   1. The number of items in the bag is in the member variable used.
//   2. For an empty bag, we do not care what is stored in any of data; for a non-empty bag,
//      the items in the bag are stored in data[0] through data[used-1], and we don't care
//      what's in the rest of data.
#include <algorithm> // Provides copy function
#include <cassert> // Provides assert function
#include "bag1.h"
using namespace std; // see namespace std;

namespace main_savitch_3
{
    const bag::size_type bag::CAPACITY;
    bag::size_type bag::erase(const value_type& target)
    {
        // See the solution to Self-Test Exercise 12 on page 147.
    }
    bool bag::erase_one(const value_type& target)
    {
        size_type index; // The location of target in the data array
        // First, set index to the location of target in the data array,
        // which could be as small as 0 or as large as used-1.
        // If target is not in the array, then index will be set equal to used.
        index = 0;
        while ((index < used) && (data[index] != target))
            ++index;
        if (index == used) // target isn't in the bag, so no work to do
            return false;
        // When execution reaches here, target is in the bag at data[index].
        // So, reduce used by 1 and copy the last item onto data[index].
        --used;
        data[index] = data[used];
        return true;
    }
}
```
```

See "Static Member Constants" on page 104 for an explanation of this line.

See Self-Test Exercise 13 for an alternative approach to this step.