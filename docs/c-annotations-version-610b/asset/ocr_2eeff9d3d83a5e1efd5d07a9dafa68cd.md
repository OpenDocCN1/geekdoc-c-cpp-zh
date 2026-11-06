```
```cpp
cout << "september -> " << months["september"] << '\\n' <<
       "april       -> " << months["april"] << '\\n' <<
       "june        -> " << months["june"] << '\\n' <<
       "november    -> " << months["november"] << '\\n';
}
/*
Generated output:
september -> 30
april     -> 30
june      -> 30
november  -> 30
*/
```
```

A comparable example, showing the use of explicitly defined hash and equality functions and key-type `char const *`:

```
```cpp
#include <unordered_map>
#include <iostream>
#include <string>
#include <cstring>
using namespace std;

struct EqualCp
{
    bool operator()(char const *l, char const *r) const
    {
        return strcmp(l, r) == 0;
    }
};
struct HashCp
{
    size_t operator()(char const *str) const
    {
        return hash<std::string const &>()(str);
    }
};
int main()
{
    unordered_map<char const *, int, HashCp, EqualCp> months;

    months["april"]    = 30;
    months["november"] = 31;

    string apr("april");    // different pointers, same string

    cout << "april      -> " << months["april"] << '\\n' <<
            "april      -> " << months[apr.c_str()] << '\\n';
}
```
```

The unordered_multimap, unordered_set and unordered_multiset containers are used analogously. For these containers the equal and hash classes must also be defined. The unordered_multimap also requires the unordered_map header file.

# 12.3.12  Regular Expressions (C++11, ?)

The C++11 standard adds handling of regular expressions to the language. Before using regular expressions as offered by the C++ standard the header file <regex> must have been included.