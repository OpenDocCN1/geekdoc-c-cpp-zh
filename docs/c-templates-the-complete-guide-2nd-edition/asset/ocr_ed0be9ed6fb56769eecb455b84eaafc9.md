us what was instantiated by which arguments and where in the code, and we see twice that we Click here to view code image

```
cannot convert from 'std::pair<const _Kty,_Ty>' to 'const std::string'
with
[
_Kty=std::string,
_Ty=double
]
```

# Missing const on Some Compilers

Unfortunately, it sometimes happens that generic code is a problem only with some compilers. Consider the following example: Click here to view code image

*basics/errornovel2.cpp*

```
#include <string>
#include <unordered_set>

class Customer
{
private:
std::string name;
public:

Customer (std::string const& n)
: name(n) {
}
std::string getName() const {
return name;
}
};
int main()
{

// provide our own hash function:
struct MyCustomerHash {
// NOTE: missing const is only an error with g++ and clang:
std::size_t operator() (Customer const& c) {
return std::hash<std::string>()(c.getName());
}
};

// and use it for a hash table of Customers:
std::unordered_set<Customer,MyCustomerHash> coll; ...
}
```

With Visual Studio 2013 or 2015, this code compiles as expected. However, with