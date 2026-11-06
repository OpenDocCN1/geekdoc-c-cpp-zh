```
        for (size_t idx = 0; idx < n; ++idx)
            iter_swap(first + idx, second + idx);

        cout << "After:\n";
        copy(first, first + n, ostream_iterator<string>(cout, " "));
        cout << '\n';
        copy(second, second + n, ostream_iterator<string>(cout, " "));
        cout << '\n';
    }
/*
    Displays:
        Before:
        alpha bravo charley
        echo foxtrot golf
        After:
        echo foxtrot golf
        alpha bravo charley
*/
```

# ### 19.1.24 lexicographical_compare

+   - **Header file:** `<algorithm>`

+   - **Function prototypes:**
+     - `bool lexicographical_compare(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, InputIterator2 last2);`
+     - `bool lexicographical_compare(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, InputIterator2 last2, Compare comp);`

+   - **Description:**
+     - The first prototype: the corresponding pairs of elements in the ranges pointed to by the ranges [first1, last1) and [first2, last2) are compared. The function returns true
+       * at the first element in the first range which is less than the corresponding element in the second range (using `operator<` of the underlying data type),
+       * if `last1` is reached, but `last2` isn't reached yet.
+   
+       `False` is returned in the other cases, which indicates that the first sequence is not lexicographically less than the second sequence. So, `false` is returned:
+       * at the first element in the first range which is greater than the corresponding element in the second range (using `operator<` of the data type to which the iterators point, reversing the operands),
+       * if `last2` is reached, but `last1` isn't reached yet,
+       * if `last1` and `last2` are reached.
+     - The second prototype: with this function the binary comparison operation as defined by `comp` is used instead of `operator<` of the data type to which the iterators point.

+   - **Example:**

```
#include <algorithm>
#include <iterator>
#include <iostream>
#include <string>
#include <cstring>
using namespace std;
```