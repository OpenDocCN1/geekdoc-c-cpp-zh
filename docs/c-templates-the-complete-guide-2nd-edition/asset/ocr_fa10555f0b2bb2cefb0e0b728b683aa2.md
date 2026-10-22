match can be found by deducing template arguments for the first template from the argument type list (A2 const*, A2*). Therefore, there is no ordering relationship between the two templates, and the call is ambiguous.

The formal ordering rules generally result in the intuitive selection of function templates. Once in a while, however, an example comes up for which the rules do not select the intuitive choice. It is therefore possible that the rules will be revised to accommodate those examples in the future.

# 16.2.4 Templates and Nontemplates

Function templates can be overloaded with nontemplate functions. All else being equal, the non-template function is preferred in selecting the actual function being called. The following example illustrates this:
details/nontmpl1.cpp

```
#include <string>
#include <iostream>

template<typename T>
std::string f(T)
{
    return "Template";
}

std::string f(int&)
{
    return "Nontemplate";
}

int main()
{
    int x = 7;
    std::cout << f(x) << '\n';  // prints: Nontemplate
}
```

details/nontmpl1.cpp

```
#include <string>
#include <iostream>

template<typename T>
std::string f(T)
{
```