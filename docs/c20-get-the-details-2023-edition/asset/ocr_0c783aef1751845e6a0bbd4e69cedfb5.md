# ### Six safe comparison functions

| Compare Function | Meaning |
|---|---|
| std::cmp_equal | == |
| std::cmp_not_equal | != |
| std::cmp_less | < |
| std::cmp_less_equal | <= |
| std::cmp_greater | > |
| std::cmp_greater_equal | >= |

Thanks to the six comparison functions, I can easily transform the previous program unsafeComparison.cpp into the program safeComparison.cpp. The new comparison functions require the header <utility>.

# ### Safe comparison of integers

```
~~~cpp
// safeComparison.cpp

#include <iostream>
#include <utility>

int main() {

    std::cout << '\n';

    std::cout << std::boolalpha;

    int x = -3;
    unsigned int y = 7;

    std::cout << " -3 == 7: " << std::cmp_equal(x, y) << '\n';
    std::cout << " -3 != 7: " << std::cmp_not_equal(x, y) << '\n';
    std::cout << " -3 < 7: " << std::cmp_less(x, y) << '\n';
    std::cout << " -3 <= 7: " << std::cmp_less_equal(x, y) << '\n';
    std::cout << " -3 > 7: " << std::cmp_greater(x, y) << '\n';
    std::cout << " -3 >= 7: " << std::cmp_greater_equal(x, y) << '\n';

    std::cout << '\n';

}
~~~
```