# 18.2 ITERATORS

+   - Given an iterator `iter`, `*iter` represents the object the iterator points to (alternatively, `iter->` can be used to reach the members of the object the iterator points to).
+   - `++iter` or `iter++` advances the iterator to the next element. The notion of advancing an iterator to the next element is consequently applied: several containers support `reversed_iterator` types, in which the `++iter` operation actually reaches a previous element in a sequence.
+   - *Pointer arithmetic* may be used with iterators of containers storing their elements consecutively in memory like vector and deque. For such containers `iter + 2` points to the second element beyond the one to which `iter` points.
+   - Merely defining an iterator is comparable to having a 0-pointer. Example:

```
```cpp
#include <vector>
#include <iostream>
using namespace std;

int main()
{
    vector<int>::iterator vi;

    cout << *vi;        // prints 0
}
```
```

STL containers usually define members offering iterators (i.e., they define their own type `iterator`). These members are commonly called `begin` and `end` and (for reversed iterators (type `reverse_iterator`)) `rbegin` and `rend`.

Standard practice requires iterator ranges to be *left* inclusive. The notation `[left, right)` indicates that `left` is an iterator pointing to the first element, while `right` is an iterator pointing just beyond the last element. The iterator range is empty when `left == right`.

The following example shows how all elements of a vector of strings can be inserted into `cout` using its iterator ranges `[begin(), end())`, and `[rbegin(), rend())`. Note that the `for`-loops for both ranges are identical. Furthermore it nicely illustrates how the auto keyword can be used to define the type of the loop control variable instead of using a much more verbose variable definition like `vector<string>::iterator` (see also section 3.3.5):

```
```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main(int argc, char **argv)
{
    vector<string> args(argv, argv + argc);

    for (auto iter = args.begin(); iter != args.end(); ++iter)
        cout << *iter << " ";
    cout << '\n';

    for (auto iter = args.rbegin(); iter != args.rend(); ++iter)
        cout << *iter << " ";
    cout << '\n';
}
```
```

Furthermore, the STL defines `const_iterator` types that must be used when visiting a series of elements in a constant container. Whereas the elements of the vector in the previous example could have been altered, the elements of the vector in the next example are immutable, and `const_iterators` are required: