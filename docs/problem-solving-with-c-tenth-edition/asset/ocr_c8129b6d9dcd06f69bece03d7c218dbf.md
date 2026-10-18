`v.reserve(32);`

sets the capacity to at least 32 elements, and

`v.reserve(v.size() + 10);`

sets the capacity to at least 10 more than the number of elements currently in the vector. Note that you can rely on `v.reserve` to increase the capacity of a vector, but it does not necessarily decrease the capacity of a vector if the argument is smaller than the current capacity.

You can change the size of a vector using the member function resize. For example, the following resizes a vector to 24 elements:

`v.resize(24);`

If the previous size was less than 24, then the new elements are initialized as we described for the constructor with an integer argument. If the previous size was greater than 24, then all but the first 24 elements are lost. The capacity is automatically increased if need be. Using resize and reserve, you can shrink the size and capacity of a vector when there is no longer any need for some elements or some capacity.

# SELF-TEST EXERCISES

+   19. Is the following program legal? If so, what is the output?

```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> v(10);
    int i;

    for (i = 0; i < v.size(); i++)
        v[i] = i;

    vector<int> copy;
    copy = v;
    v[0] = 42;

    for (i = 0; i < copy.size(); i++)
        cout << copy[i] << " ";
    cout << endl;

    return 0;
}
```
```

+   20. What is the difference between the size and the capacity of a vector?