Inspecting all of the possible types within a variant quickly devolves into a redundant chain of if statements. For example, the following prints the value of a `Variant<int, double, string>` named `v`:

**Click here to view code image**

```
```cpp
if (v.index()!=1) {
    std::cout << v.get<int>();
}
else if (v.is<double>()) {
    std::cout << v.get<double>();
}
else {
    std::cout << v.get<string>();
}
```
```

To generalize this to print the value stored in an arbitrary variant requires a recursively instantiated function template along with a helper. For example:

**Click here to view code image**

```
```cpp
// variant/printrec.cpp
#include <variant.hpp>
#include <iostream>

template<typename V, typename Head, typename... Tail>
void printImpl(V const& v)
{
    if (v.template is<Head>()) {
        std::cout << v.template get<Head>();
    }
    else if constexpr (sizeof...(Tail) > 0) {
        printImpl<V, Tail...>(v);
    }
}

template<typename... Types>
void print(variant<Types...> const& t)
{
    printImpl<variant<Types...>, Types...>(t);
}

int main()
{
    variant<int, short, float, double> v(1.5);
    print(v);
}
```
```

This is a significant amount of code for a relatively simple operation. To simplify this, we turn the problem around by extending `Variant` with a `visit()` operation. The client then passes in a visitor function object whose `operator()` will be invoked with the active value. Because the value could be any one of the variant's potential types, this operator is likely either to be overloaded or itself a function template. For example, a generic lambda provides a templated `operator()`, allowing us to easily represent the print operation for a variant:

**Click here to view code image**

```
```cpp
v.visit([](auto const& value) {
    std::cout << value;
});
```
```

This generic lambda is roughly equivalent to the following function object, which can also be useful for compilers that do not yet support generic lambdas:

**Click here to view code image**

```
```cpp
class VariantPrinter {
public:
    template<typename T>
    void operator()(T const& value) const
    {
        std::cout << value;
    }
};
```
```

The core of the `visit()` operation is similar to the process in our `get` operation. It steps through the types of the variant, checking whether the active...