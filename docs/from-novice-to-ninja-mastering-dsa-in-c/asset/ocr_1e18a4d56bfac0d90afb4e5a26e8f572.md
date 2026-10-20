# Vector:-

```
#include <vector>

std::vector<int> numbers = {1, 2, 3, 4, 5};
numbers.push_back(6);
```

# List:-

```
#include <list>

std::list<double> values = {1.1, 2.2, 3.3, 4.4};
values.push_back(5.5);
```

# Deque:-

```
#include <deque>

std::deque<char> characters = {'a', 'b', 'c'};
characters.push_front('z');
```

# Map:-

```
#include <map>

std::map<std::string, int> ages = {{"Alice", 25}, {"Bob", 30}};
ages["Charlie"] = 28;
```

# Algorithms:

STL algorithms operate on containers, providing a rich set of functions for common operations like sorting, searching, and modifying elements. Algorithms are designed to work with iterators, providing a consistent interface for various container types.

# Sorting:-

```
#include <algorithm>

std::vector<int> numbers = {5, 2, 8, 1, 3};
std::sort(numbers.begin(), numbers.end());
```