```
```cpp
struct CustomerEq
{
    bool operator() (Customer const& c1, Customer const& c2) const
    {
        return c1.getName() == c2.getName();
    }
};

struct CustomerHash
{
    std::size_t operator() (Customer const& c) const
    {
        return std::hash<std::string>()(c.getName());
    }
};

// define class that combines operator() from variadic
// template parameters

template<typename... Bases>
struct Overloader : Bases...
{
    using Bases::operator()...;    // OK since C++17
};

int main()
{
    // combine hashes and equality for customers in one
    using CustomerOP = Overloader<CustomerHash, CustomerEq>;

    std::unordered_set<Customer, CustomerHash, CustomerEq> customers;
    std::unordered_set<Customer, CustomerOP, CustomerOP> customers2;
}
```
```

Here, we first define a class Customer and independent function objects to hash and compare Customer objects. With

Click here to view code image

```
```cpp
template<typename... Bases>
struct Overloader : Bases...
{
    using Bases::operator()...;    // OK since C++17
};
```
```

we can define a class derived from a variable number of base classes that brings in the operator() declarations from each of those base classes. With

Click here to view code image

```
```cpp
using CustomerOP = Overloader<CustomerHash, CustomerEq>;
```
```

we use this feature to define Customer objects with both CustomerHash and CustomerEq and enable both implementations of operator() in the derived class.

See Section 26.4.2 for another application of this technique.

# 4.5 SUMMARY

+   - By using parameter packs, templates can be defined for an arbitrary number of template parameters of arbitrary type.
+   - To process the parameters, you need recursion and/or a matching non-variadic function.
+   - Operator `sizeof...` yields the number of arguments provided for a parameter pack.
+   - A typical application of variadic templates is forwarding an arbitrary number of arguments of arbitrary type.
+   - By using fold expressions, you can apply operators to all elements of a parameter pack.

+   1. Initially, in C++11 and C++14 this was an ambiguity, which was fixed later (see Core Issue 1558), but all compilers handled it this way in all versions.