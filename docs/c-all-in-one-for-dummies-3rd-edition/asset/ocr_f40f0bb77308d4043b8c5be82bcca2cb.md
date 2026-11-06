| Data Type | Prefix | Suffix | Resultant Type |
|---|---|---|---|
| int | ULL, U1, ull, uLL, LLU, LLu, 1LLU, or llu |  | unsigned long |
| double | F or f |  | float |
| double | L or l |  | long double |
| char |  | L | wchar_t |
| char |  | U | char32_t |
| char |  | u | char16_t |
| String |  | L | wchar_t const* |
| String |  | U | char32_t const* |
| String |  | u | char16_t const* |

Using the prefixes and suffixes can save you considerable time. The PrefixesAndSuffixes example in Listing 2-1 demonstrates how you'd employ them to create variables of various sorts.

# ### Listing 2-1: Creating Literals Using Prefixes and Suffixes

```
~~~cpp
#include <typeinfo>
#include <cxxabi.h>

using namespace std;
using namespace abi;

char* Demangle(const char* Object)
{
    int Status;
    char* RealName;

    RealName = __cxa_demangle(Object, 0, 0, &Status);
    return RealName;
}

int main()
{
    auto Int1 = 23;
    auto Int2 = 23l;
    auto Int3 = 23U;
    auto Int4 = 23u;

    auto String1 = "Hello";
    auto String2 = u8"Hello";
    auto String3 = U"Hello";
    auto String4 = u"Hello";

    cout << Int1 << endl << Demangle(typeid(Int1).name()) << endl;
    cout << Int2 << endl << Demangle(typeid(Int2).name()) << endl;
~~~
```