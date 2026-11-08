whether a type has a value_type or a char_type, type member type is false.

Click here to view code image

```
```cpp
#include "bool_type.hpp"

#include <iostream>
#include <vector>

DEFINE_HAS_TYPE(value_type);
DEFINE_HAS_TYPE(char_type);

int main()
{
    std::cout << "int::value_type: "
              << HasType_value_type<int>::value << '\n';
    std::cout << "float::value_type: "
              << HasType_value_type<float>::value << '\n';
    std::cout << "std::vector<int>::value_type: "
              << HasType_value_type<std::vector<int>>::value << '\n';
    std::cout << "std::vector<char>::value_type: "
              << HasType_value_type<std::vector<char>>::value << '\n';
}
```
```

# ### 9.4.3 Detecting Nontype Members

We can modify the trait to check for data members and (single) member functions.

Click here to view code image

```
```cpp
#include "hasmember.hpp"

DEFINE_HAS_MEMBER(member)

template<typename T, typename = std::void_t<>>
struct HasMember : std::false_type {
};

template<typename T>
struct HasMember<T, std::void_t<decltype(T::member)>> {
    static bool const value = true;
};
```
```

Here, we use SFINAE to disable the partial specialization when &T::member is not valid. For that construct to be valid the following must be true:

+   - Member must unambiguously identify a member of T (e.g., it cannot be an overloaded member function name, or the name of multiple inherited members of the same name).
+   - The member must be accessible.
+   - The member must be a nontype, nonenumerator member (otherwise the prefix & would be ill-formed).
+   - If T is a class, the type must not provide an operator& that returns a different type (such as a weirdly overloaded operator&). However, we can then replace &T::member with std::addressof(T::member) (or similar) to still make that operator work.

Click here to view code image

```
```cpp
#include "hasmember.hpp"

#include <iostream>
#include <vector>
#include <utility>
```
```