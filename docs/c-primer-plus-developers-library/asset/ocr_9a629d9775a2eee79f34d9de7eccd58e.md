Given a pair object, you can access the two components by using the `first` and `second` members:

```
pair<const int, string> item(213, "Los Angeles");
cout << item.first << ' ' << item.second << endl;
```

What about getting information about a multimap object? The `count()` member function takes a key as its argument and returns the number of items that have that key. The `lower_bound()` and `upper_bound()` member functions take a key and work as they do for set. Also the `equal_range()` member function takes a key as its argument and returns iterators representing the range matching that key. In order to return two values, the method packages them into a pair object, this time with both template arguments being the iterator type. For example, the following would print a list of cities in the codes object with area code 718:

```
pair<multimap<KeyType, string>::iterator,
     multimap<KeyType, string>::iterator> range
                         = cities.equal_range(718);
```

```
cout << "Cities with area code 718:\n";
std::multimap<KeyType, std::string>::iterator it;
for (it = range.first; it != range.second; ++it)
    cout << (*it).second << endl;
```

Declarations like those just listed helped motivate the C++11 automatic type deduction feature, which allows you to simplify the code as follows:

```
auto range = cities.equal_range(718);
cout << "Cities with area code 718:\n";
for (auto it = range.first; it != range.second; ++it)
    cout << (*it).second    << endl;
```

Listing 16.14 demonstrates most of these techniques. It also uses typedef to simplify some of the code writing.

# Listing 16.14  `multmap.cpp`

```
// multmap.cpp -- use a multimap
#include <iostream>
#include <string>
#include <map>
#include <algorithm>

typedef int KeyType;
typedef std::pair<const KeyType, std::string> Pair;
typedef std::multimap<KeyType, std::string> MapCode;

int main()
{

```