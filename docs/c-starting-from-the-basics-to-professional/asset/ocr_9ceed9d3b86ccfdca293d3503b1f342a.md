Ex19_05 is yet another variant of Ex19_02 and Ex19_03, only this time one that uses lambda expressions to define all its callback functions:

```
```cpp
// Ex19_05.cpp
// Exercising the use of lambda expressions as callback functions
import <iostream>;
import <string>;
import <string_view>;
import <optimum>;

int main()
{
    std::vector numbers{ 91, 18, 92, 22, 13, 43 };
    std::cout << "Minimum element: "
              << *findOptimum(numbers, [](int x, int y) { return x < y; }) << std::endl;
    std::cout << "Maximum element: "
              << *findOptimum(numbers, [](int x, int y) { return x > y; }) << std::endl;

    // Define two anonymous comparison functions for strings:
    auto alpha = [](std::string_view x, std::string_view y) { return x > y; };
    auto longer = [](std::string_view x, std::string_view y) { return x.size() > y.size(); };

    std::vector<std::string> names{ "Moe", "Larry", "Shemp", "Curly", "Joe", "Curly Joe" };
    std::cout << "Alphabetically last name: " << *findOptimum(names, alpha) << std::endl;
    std::cout << "Longest name: " << *findOptimum(names, longer) << std::endl;
}
```
```

The result will be the same as before. Clearly, if you only need to sort strings on their length once, a lambda expression is more convenient than defining a separate longer() function and definitely far more interesting than defining a longer functor class.

> **Tip** If <functional> defines a suitable functor type, using that type is normally far more compact and readable than a lambda expression. std::less<> and std::greater<>, for instance, could readily replace the first three lambda expressions in Ex19_05.cpp (see also Ex19_05A).

# # Generic Lambdas

A generic lambda is a lambda expression where at least one placeholder type such as auto, auto&, or const auto& is used as a parameter type. Doing so effectively turns the function call operator of the generated class into a template. Precisely as if you would have used the abbreviated function template syntax (see Chapter 10) for this member function. In Ex19_05, for instance, you could replace the definitions of the alpha and longer variables with the following (you best not use plain auto as placeholder here, because then strings would needlessly be copied during sorting):

```
```cpp
auto alpha = [](const auto& x, const auto& y) { return x > y; };
auto longer = [](const auto& x, const auto& y) { return x.length() > y.length(); };
```
```