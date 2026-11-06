```
```cpp
string remaining[size];

copy
(
    remaining,
    replace_copy(words, words + size, remaining, string("alpha"),
                                             string("ALPHA")),
    ostream_iterator<string>(cout, " ")
);
cout << '\n';
}
/*
    Displays:
        kilo ALPHA lima mike ALPHA november ALPHA oscar ALPHA ALPHA papa
*/
```
```

# ### 19.1.46 `replace_copy_if`

+   - Header file: `<algorithm>`
+   - Function prototypes:
+     - `OutputIterator replace_copy_if(ForwardIterator first, ForwardIterator last, OutputIterator result, UnaryPredicate pred, Type const &value);`
+   - Description:
+     - The elements in the range pointed to by `[first, last)` are copied to the range `[result, returnvalue)`, where `returnvalue` is the value returned by the function. The elements for which the unary predicate `pred` returns `true` are replaced by `value`. The range `[first, last)` is not modified.

+   - Example:

```
```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <functional>
#include <iterator>
using namespace std;

int main()
{
    string words[] =
        { "kilo", "alpha", "lima", "mike", "alpha", "november",
          "alpha", "oscar", "alpha", "alpha", "papa" };
    size_t const size = sizeof(words) / sizeof(string);
    string result[size];

    // Note: the comparisons are: "mike" > word[i]
    replace_copy_if(words, words + size, result,
                    bind1st(greater<string>(), string("mike")),
                    string("ALPHA"));
    copy (result, result + size, ostream_iterator<string>(cout, " "));
    cout << '\n';
}
/*
    Displays (all strings in words[] which are exceeded by ‘mike’ are
        replaced by ALPHA):
        ALPHA ALPHA ALPHA mike ALPHA november ALPHA oscar ALPHA ALPHA papa
*/
```
```