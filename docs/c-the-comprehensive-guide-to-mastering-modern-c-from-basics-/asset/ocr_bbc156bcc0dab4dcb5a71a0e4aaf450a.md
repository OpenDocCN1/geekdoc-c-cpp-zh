```
#ifndef PERSON HPP
#define PERSON HPP
#include <string>
#include <iostream> // ostream
struct Person {
    std::string name;
    int age;
    std::string city;
    std::ostream& print(std::ostream& os);
};
#endif // PERSON HPP
```

```
#include "person.hpp"
#include <format>
using std::ostream; using std::format;
ostream& Person::print(ostream& os) {
    return os << format("{{\}}") from {"}}"{\}\n", name, age, city);
}
```

# Figure 12.2 Splitting a class into the header and implementation.