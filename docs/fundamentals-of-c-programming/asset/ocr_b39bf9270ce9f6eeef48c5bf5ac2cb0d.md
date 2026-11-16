```
case TextType::Fixed:
case TextType::Bounded:
    return text;
case TextType::Fancy:
    return left_bracket + text + right_bracket;
default:
    return "UNKNOWN TYPE";
}
}

void AltText2::append(const std::string& extra) {
switch (type) {
case TextType::Plain:
    text += extra; // Just concatenate
    break;
case TextType::Fancy:
    text += connector + extra; // Join with connector
    break;
case TextType::Fixed:
    break; // Ignore attempt to append
case TextType::Bounded:
    // Ensure the length does not exceed the established limit
    int avail = length_limit - text.length();
    text += extra.substr(0, avail);
    break;
}
}
```

Listing 17.16 (testalttext2.cpp) demonstrates that our new bounded text object does indeed limit the length of its enclosed string field.

# Listing 17.16: testalttext2.cpp

```
#include <string>
#include <vector>
#include <iostream>
#include "alttext2.h"

int main() {
std::vector<AltText2> texts { {TextType::Plain, "Wow"},
{TextType::Fancy, "Wee", "[", "]", "-"},
{TextType::Fixed},
{TextType::Bounded, "XYZ", 5},
{TextType::Fancy, "Whoa", "-:", "-:", "-:"} };

for (auto t : texts)
std::cout << t.get() << " \n";
for (auto& t : texts) {
t.append("A");
t.append("B");
t.append("C");
t.append("D");
t.append("E");
t.append("F");
}
}
```