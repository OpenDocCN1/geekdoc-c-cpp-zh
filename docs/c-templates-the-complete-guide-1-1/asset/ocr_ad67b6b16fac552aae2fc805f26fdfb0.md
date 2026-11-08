```
```cpp
DEFINE_HAS_MEMBER(size);
DEFINE_HAS_MEMBER(first);

int main()
{
    std::cout << "has:size: "
              << HasMemberT_size<int>::value << '\n';

    std::cout << "has:vector:size? "
              << HasMemberT_size<std::vector<int>>::value;

    std::cout << "std::pair<int,int>::first: "
              << HasMemberT_first<std::pair<int,int>>::value;
}
```
```

It would not be difficult to modify the partial specialization to exclude classes where T::member is not a pointer-to-member type (which means a non-static data member). Similarly, a pointer-to-member function could be excluded or required to limit the trait to data members or member functions.

# Detecting Member Functions

Note that the isMember trait only checks whether a single member with the corresponding name exists. That trait also will fail if two members exist, which might happen if we check for overloaded member functions. For example:

Click here to view code image

```
```cpp
DEFINE_HAS_MEMBER(begin);
std::cout << HasMemberT_begin<int>::value; // false
```
```

However, as explained in Section 8.4.1 on page 133, the SFINAE principle protects against attempts to create bad template types and expressions in function template declarations, allowing the overloading technique above to extend to testing whether arbitrary expressions are well-formed.

That is, we can simply check whether we can call a function of interest in a specific way and that can succeed even if the function is overloaded. As with the IsConvertible<> trait in Section 9.5 on page 428, the trick is to formulate the expression that checks whether we can call begin() inside a call to expression for the default value of an additional function template parameter:

Click here to view code image

traits/hasbegin.hpp

```
```cpp
#include <utility>      // for declval
#include <type_traits>   // for true_type, false_type

// primary template:
template<typename, typename = std::void_t<>>
struct HasBeginT : std::false_type
{
};

// partial specialization (may be SFINAE'd away):
template<typename T>
struct HasBeginT<T, std::void_t<decltype(std::declval<T>().begin())>>
  : std::true_type
{
};
```
```

# Here we use

Click here to view code image

traits/hasbegin.hpp

```
```cpp
decltype(std::declval<T>().begin())
```
```

to test whether, given a value/object of type T (using std::declval to avoid constructing a type), calling a member begin() is valid.

# Detecting Other Expressions

We can use the technique above for other kinds of expressions and even compile multiple expressions. For example, we can test whether, given types T and U, there is a suitable < operator defined for values of these types.

Click here to view code image