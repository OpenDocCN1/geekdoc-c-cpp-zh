```
```cpp
template <std::random_access_iterator I, std::sentinel_for<I> S,
    class Comp = ranges::less, class Proj = std::identity>
requires std::sortable<I, Comp, Proj>
constexpr I sort(I first, S last, Comp comp = {}, Proj proj = {});

template <ranges::random_access_range R, class Comp = ranges::less,
    class Proj = std::identity>
requires std::sortable<ranges::iterator_t<R>, Comp, Proj>
constexpr ranges::borrowed_iterator_t<R> sort(R&& r, Comp comp = {}, Proj proj = {});
```
```

When you study the second overload, you notice that it takes a sortable range R, a predicate Comp, and a projection Proj. The predicate Comp uses for default less, and the projection Proj the identity std::identity that does return its arguments unchanged. A projection is a mapping of a set into a subset. A projection can be

+   - a callable such as a lambda
+   - a pointer to a member function or data member

Let me show you what that means:

# ### Applying projections on data types

```
```cpp
// rangeProjection.cpp

#include <algorithm>
#include <functional>
#include <iostream>
#include <vector>

struct PhoneBookEntry{
    std::string name;
    int number;
};

void printPhoneBook(const std::vector<PhoneBookEntry>& phoneBook) {
    for (const auto& entry: phoneBook) std::cout << "(" << entry.name << ", "
        << entry.number << ")";
    std::cout << "\n\n";
}

int main() {

    std::cout << '\n';

    std::vector<PhoneBookEntry> phoneBook{ {"Brown", 111}, {"Smith", 444},
```
```

*https://en.cppreference.com/w/cpp/utility/functional/identity