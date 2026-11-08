```
```cpp
const auto& larger(const double& a, const int& b)
{
    return a > b ? a : b;    // Warning: returning a reference to a temporary double!!!
}
```
```

Here a > b ? a : b creates a new temporary value of type double (the so-called *common type* of int and double). And of course we taught you better than to return a reference or pointer to a local or temporary variable like that (see Chapter 8)!

The solution to such predicaments, where neither auto or const auto& is appropriate, is the more advanced decltype(auto) placeholder type. When used as the return type of a function, this placeholder evaluates to the exact type of the expression(s) in the return statement(s). You could therefore create an improved version of the larger<> template as follows (see also EX10_03A).

```
```cpp
template <typename T1, typename T2>
decltype(auto) larger(const T1& a, const T2& b)
{
    return a > b ? a : b;
}
```
```

For larger<double, int>(), the deduced return type will then still be double, but that of larger<std::vector<int>, std::vector<int>>() will be const std::vector<int>&—as desired!

Note that you should only use decltype(auto) in templates. In non-generic code, you should always explicitly choose between the more specific auto or (const) auto& instead.

# Default Values for Template Parameters

You can specify default values for function template parameters. For example, you could specify double as the default return type in the prototype for the template introduced earlier like this:

```
```cpp
// Template with default value for the first parameter
template <typename ReturnType=double, typename T1, typename T2>
ReturnType larger(const T1&, const T2&);
```
```

If you don’t specify any template parameter values, the return type will be double. Note that we only use this example to introduce default values for template parameters, not because it is necessarily a good idea to define larger() like this. The reason this is not such a great idea is that default, double, is not always what you want. The larger() function resulting from the following statement, for instance, accepts arguments of type int and returns the result as type double:

```
```cpp
std::cout << larger(123, 543) << std::endl;
```
```

The main point we want to convey with this example is that you can specify default values for template arguments at the beginning of the template argument list. You’ll recall that for function parameters it was only possible to define default values at the end of the list. You have quite some more flexibility when specifying default values for template parameters. In our first example, ReturnType is the first in the list. But you can also specify default values for parameters in the middle of the list or at the end. Here is yet another larger() template to illustrate the latter:

```
```cpp
// Template with a default value referring to an earlier parameter
template <typename T, typename ReturnType=T>
ReturnType larger(const T&, const T&);
```
```