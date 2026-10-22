```
template<typename T>
struct IsFundaT : std::false_type {
static constexpr bool value = false;
};
```

For each fundamental type, a specialization is defined so that IsFundaT<T>::value is true. We define a macro that expands to the necessary code for convenience. For example: Click here to view code image

```
MK_FUNDA_TYPE(bool)
```

expands to the following:

Click here to view code image

```
template<> struct IsFundaT<bool> : std::true_type {
static constexpr bool value = true;
};
```

The following program demonstrates a possible use of this template: Click here to view code image

traits/isfundatest.cpp

```
#include "isfunda.hpp"
#include <iostream>

template<typename T>
void test (T const&)
{
if (IsFundaT<T>::value) {
std::cout << "T is a fundamental type" << '\n';
}
else {
std::cout << "T is not a fundamental type" << '\n';
}
}

int main()
{
test(7);
test("hello");
}
```

It has the following output:

Click here to view code image

```
T is a fundamental type
T is not a fundamental type
```

In the same way, we can define type functions IsIntegralT and