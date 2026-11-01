```
std::chrono::system_clock::now())
, query(std::move(query_))
{}
```

You could optionally call **population** in the constructor body. Given that it is an expensive function that requires caching, though, we would not call it until the value was needed.

The other way to fix the problem is to reorder the member data in the class defini-tion, thus:

[Click here to view code image](#)

```
class population_service {
public:
    population_service(std::string query_);
    float population() const;

private:
    std::string query;
    mutable std::time_t expiry;
    mutable float current_population;
};
```

With this ordering, **population** can be safely invoked in the initialization list, although for the same reason I would not do this.

This leads us to an interesting aside about class layout and alignment. Consider this program:

[Click here to view code image](#)

```
#include <iostream>
struct int_two_bools {
    bool m_b1;
    int m_i;
    bool m_b2;
```