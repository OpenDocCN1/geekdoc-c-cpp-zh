parameter, and the function would work with any range and container that supports rbegin(). If I were more careful, I wouldn't traverse the entire sequence from start to finish, but only up to the halfway point, because == should be symmetric. I could achieve this by writing the following instead of s.end(): s.begin()+(s.end()-s.begin())/2.

In the case of for_each, information is not the goal; rather, a unary function without a return value is called on each element. Actually, these functions are intended to be read-only. However, if you provide an (in)appropriate functor or predicate, you can indeed modify the elements of the range. So doing so forbidden but probably confusing. With for_each, you can see an example in Listing 25.11. Instead, you should use transform here.

```
// https://godbot.org/z/iz1Ggo7d9
#include <iostream>
#include <vector>
#include <algorithm>
int main() {
    std::vector<int> c{1,2,3,4};
    std::for_each(c, [](auto &n) { n*=n; }); // Not modifying
    std::cout << c[3] << "\n"; // Output: 16
}
```

**Listing 25.11** Even "read-only" algorithms like "for_each" can modify elements.

That is why I want to emphasize one thing: do not use for_each to solve every problem. There are often algorithms that are better at solving certain problems. And if you look at the list of algorithms from time to