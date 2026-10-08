scope:
Click here to view code image

```
using namespace std;
```

```
void g(vector<int> &v) {
    sort(v.begin(),v.end()); // OK
    sort(v); // II error: no matching function (in std)
    ranges::sort(v); // OK
    using ranges::sort;
    (v) OK here on
    sort(v); // OK
}
```

# 9.3.3 Modules

There are not yet standard-library modules. C++23 is likely to remedy this omission (caused by lack of committee time). For now, I module std that is likely to become standard, offering all facilities from namespace std. See Appendix A.

# 9.3.4 Headers

Here is a selection of standard-library headers, all supplying declarations in namespace std:

| Selected Standard Library Headers | |
|---|---|
| <algorithm> | copy(), find(), sort() | Chapter 13 |
| <array> | array | $15.3.1 |
| <chrono> | duration, time_point, month, time_zone | $16.2 |
| <cmath> | sqrt(pow), | $17.2 |
| <complex> | complex, sqrt(pow), | $17.4 |
| <concepts> | floating_point, copyable, predicate, invocable | $14.5 |
| <filesystem> | path | $11.9 |
| <format> | format() | $11.6.2 |
| <fstream> | fstream, ifstream, ofstream | $11.7.2 |
| <functional> | function, greater_equal, hash, range_value_t | Chapter 16 |
| <future> | future, promise | $18.5 |
| <ios> | hex, dec, scientific, fixed, defaultfloat | $11.6.2 |
| <iostream> | istream, ostream, cin, cout | Chapter 11 |
| <map> | map, multimap | $12.6 |
| <memory> | unique_ptr, shared_ptr, allocator | $15.2.1 |
| <random> | default_random_engine, normal_distribution | $17.5 |
| <ranges> | sized_range, subrange, take(), split(), iterator_t | $14.1 |