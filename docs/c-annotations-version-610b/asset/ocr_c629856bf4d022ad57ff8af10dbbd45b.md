```
~~~cpp
using namespace std;

class NaturalSquares
{
    size_t d_newsqr;
    size_t d_last;

    public:
        NaturalSquares(): d_newsqr(0), d_last(0)
        {}
        size_t operator()()
        {                         // using: (a + 1)^2 == a^2 + 2*a + 1
            return d_newsqr += (d_last++ << 1) + 1;
        }
};
int main()
{
    vector<size_t>    uv(10);

    generate_n(uv.begin(), 5, NaturalSquares());

    copy(uv.begin(), uv.end(), ostream_iterator<int>(cout, " "));
    cout << '\n';
}
// Displays:   1 4 9 16 25 0 0 0 0 0
~~~
```

# ### 19.1.20 includes

+   - Header file: `<algorithm>`
+   - Function prototypes:
+     - `bool includes(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, InputIterator2 last2);`
+     - `bool includes(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, InputIterator2 last2, Compare comp);`
+   - Description:
+     - The first prototype: both sequences of elements implied by the ranges `[first1, last1)` and `[first2, last2)` should have been sorted using the `operator<` of the data type to which the iterators point. The function returns `true` if every element in the second sequence `[first2, last2)` is contained in the first sequence `[first1, last1)` (the second range is a subset of the first range).
+     - The second prototype: both sequences of elements implied by the ranges `[first1, last1)` and `[first2, last2)` should have been sorted using the `comp` function object. The function returns `true` if every element in the second sequence `[first2, last2)` is contained in the first sequence `[first1, last1)` (the second range is a subset of the first range).
+   - Example:

```
~~~cpp
#include <algorithm>
#include <string>
#include <cstring>
#include <iostream>
using namespace std;

class CaseString
{
~~~
```