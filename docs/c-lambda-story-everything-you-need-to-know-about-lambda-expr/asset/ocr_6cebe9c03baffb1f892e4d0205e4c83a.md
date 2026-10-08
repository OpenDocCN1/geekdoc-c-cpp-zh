the given value.
- std::bind2nd - creates a callable object with the second argument fixed
to the given value.
- and many more.

Let's write some code that benefits from the helpers:

Using old C++98/03 functional helpers. Live code @Wandbox

```
#include <algorithm>
#include <functional>
#include <vector>

int main() {
    std::vector<int> v;
    v.push_back(1);
    v.push_back(2);
    // push_back until 9...
    const size_t smaller5 = std::count_if(v.begin(), v.end(),
        std::bind2nd(std::less<int>(),), 5));

    return smaller5;
}
```

The example uses std::bind2nd and fixes its second argument by using
std::bind2nd. This whole "composition" is passed into count_if. As you
can probably guess, the code expands into a function that performs a simple
comparison:

return x < 5;

If you wanted ready-to-use helpers, then you can also look at the boost
library, for example boost::bind.

Unfortunately, the main issue with this approach is the complexity and hard-
to-learn syntax. for instance writing code that composes two or more
functions is not natural. Have a look below:

Composing functional helpers. Live Code @Wandbox

```
std::vector<int> v;
v.push_back(1);
v.push_back(2);
// push_back until 9...
const size_t val = std::count_if(v.begin(), v.end(),
    std::bind(std::logical_and<bool>(),),
    std::bind(std::greater<int>(),_1, 2),
    std::bind(std::less_equal<int>(),_1, 6)));
```