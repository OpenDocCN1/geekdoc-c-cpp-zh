```
```cpp
// skip leading zeros
for (i = 0; i < HugeInteger::digits && 0 == num.integer[i]; ++i) { }

if (i == HugeInteger::digits) {
    output << 0;
}
else {
    for (; i < HugeInteger::digits; ++i) {
        output << num.integer[i];
    }
}

return output;
}
```
```

**Fig. 11.13** | HugeInteger member-function and friend-function definitions. (Part 3 of 3.)

```
```cpp
// fig11_14.cpp
// HugeInteger test program.
#include <iostream>
#include "HugeInteger.h"

int main() {
    HugeInteger n1{7654321};
    HugeInteger n2{7891234};
    HugeInteger n3{"99999999999999999999999999999999999999"};
    HugeInteger n4{"1"};
    HugeInteger n5{};

    std::cout << "n1: " << n1 << "\nn2: " << n2 << "\nn3: " << n3
              << "\nn4: " << n4 << "\nn5: " << n5 << "\n\n";

    n5 = n1 + n2;
    std::cout << n1 << " + " << n2 << " = " << n5 << "\n\n";

    std::cout << n3 << " + " << n4 << " = " << (n3 + n4) << "\n\n";

    n5 = n1 + 9;
    std::cout << n1 << " + " << 9 << " = " << n5 << "\n\n";

    n5 = n2 + "10000";
    std::cout << n2 << " + " << "10000" << " = " << n5 << "\n";
}
```
```

```
```text
n1: 7654321
n2: 7891234
n3: 99999999999999999999999999999999999999{}
n4: 1
n5: 0

7654321 + 7891234 = 15545555
```
```

**Fig. 11.14** | HugeInteger test program. (Part 1 of 2.)