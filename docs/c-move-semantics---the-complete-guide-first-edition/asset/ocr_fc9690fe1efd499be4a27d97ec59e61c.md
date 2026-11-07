```
```cpp
Person(Person&& p) noexcept  // guarantee not to throw
    : name{std::move(p.name)} {
    std::cout << "MOVE " << name << '\n';
}
...
};
```
```

If we now use Persons in the same way as before:

`basics/personmove.cpp`

```
```cpp
#include "personmove.hpp"
#include <iostream>
#include <vector>

int main()
{
    std::vector<Person> coll{"Wolfgang Amadeus Mozart",
                             "Johann Sebastian Bach",
                             "Ludwig van Beethoven"};
    std::cout << "capacity: " << coll.capacity() << '\n';
    coll.push_back("Pjotr Iljitsch Tschaikowski");
}
```
```

we get the following output:

```
```text
COPY Wolfgang Amadeus Mozart
COPY Johann Sebastian Bach
COPY Ludwig van Beethoven
capacity: 3
MOVE Pjotr Iljitsch Tschaikowski
MOVE Wolfgang Amadeus Mozart
MOVE Johann Sebastian Bach
MOVE Ludwig van Beethoven
```
```

Again, we first copy the initial values into the vector

![](bbox=[0.115, 0.727, 0.588, 0.853])

However, as the last three rows of the output visualize, the vector now uses the move constructor to move its elements to the new reallocated memory: