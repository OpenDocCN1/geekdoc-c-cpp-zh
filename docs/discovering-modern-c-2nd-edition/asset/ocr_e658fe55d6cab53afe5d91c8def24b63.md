```
```cpp
#include <initializer_list>
#include <algorithm>

class vector
{
// ...
vector(std::initializer_list<double> values)
: my_size{values.size()}, data{new double[my_size]}
{
    copy(begin(values), end(values), data);
}

vector& operator=(std::initializer_list<double> values)
{
    assert(my_size == values.size());
    copy(begin(values), end(values), data);
    return *this;
}
};
```
```