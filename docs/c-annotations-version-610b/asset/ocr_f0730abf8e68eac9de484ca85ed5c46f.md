The interfaces required for other iterator types are simpler, requiring only a subset of the interface required by a random access iterator. E.g., the forward iterator is never decremented and never incremented over arbitrary step sizes. Consequently, in that case all decrement operators and `operator+(int step)` can be omitted from the interface. Of course, the tag to use would then be `std::forward_iterator_tag`. The tags (and the set of required operators) vary accordingly for the other iterator types.

# ## 21.13.2 Implementing a `reverse_iterator`

Once we've implemented an iterator, the matching *reverse iterator* can be implemented in a jiffy. Comparable to the `std::iterator` a `std::reverse_iterator` exists, that nicely implements the reverse iterator for us once we have defined an iterator class. Its constructor merely requires an object of the iterator type for which we want to construct a reverse iterator.

To implement a reverse iterator for `StringPtr` we only need to define the `reverse_iterator` type in its interface. This requires us to specify only one line of code, which must be inserted after the interface of the class iterator:

```
~~~cpp
typedef std::reverse_iterator<iterator> reverse_iterator;
~~~
```

Also, the well known members `rbegin` and `rend` are added to `StringPtr`'s interface. Again, they can easily be implemented inline:

```
~~~cpp
inline StringPtr::reverse_iterator StringPtr::rbegin()
{
    return reverse_iterator(end());
}
inline StringPtr::reverse_iterator StringPtr::rend()
{
    return reverse_iterator(begin());
}
~~~
```

Note the arguments the `reverse_iterator` constructors receive: the *begin point* of the reversed iterator is obtained by providing `reverse_iterator`'s constructor with the value returned by the member `end`: the *endpoint* of the normal iterator range; the *endpoint* of the reversed iterator is obtained by providing `reverse_iterator`'s constructor with the value returned by the member `begin`: the *begin point* of the normal iterator range.

The following small program illustrates the use of `StringPtr`'s `RandomAccessIterator`:

```
~~~cpp
#include <iostream>
#include <algorithm>
#include "stringptr.h"
using namespace std;

int main(int argc, char **argv)
{
    StringPtr sp;

    while (*argv)
        sp.push_back(new string(*argv++));

    sort(sp.begin(), sp.end());
    copy(sp.begin(), sp.end(), ostream_iterator<string>(cout, "  "));

    cout << "\n========\n";

    sort(sp.rbegin(), sp.rend());
~~~
```