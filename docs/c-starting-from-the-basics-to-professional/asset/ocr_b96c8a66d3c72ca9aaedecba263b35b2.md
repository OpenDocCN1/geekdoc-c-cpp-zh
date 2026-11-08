Both options are demonstrated in our next example:

```
```cpp
// Ex19_03.cpp
// Exercising the use of a functor as callback functions
import <iostream>;
import optimum;
import less;

template <typename T>
bool greater(const T& one, const T& other) { return one > other; }

int main()
{
    less less;

    std::vector numbers{ 91, 18, 92, 22, 13, 43 };
    std::cout << "Minimum element: " << *findOptimum(numbers, less) << std::endl;
    std::cout << "Maximum element: " << *findOptimum(numbers, greater<int>) << std::endl;
}
```
```

# Standard Function Objects

You can customize many templates of the Standard Library by providing them with a first-class function, similar to what you did with `findOptimum()` in examples Ex19_02 and Ex19_03. For regular functions you can mostly use a plain function pointer, but for built-in operators that is not an option. You cannot create a pointer to a built-in operator. Of course, it is easy to quickly define either a function (as in Ex19_02) or a functor class (Less in Ex19_03) that emulates the operator's behavior, but doing so for every operator all the time would become tedious very fast.

Of course, this did not escape the designers of the Standard Library either. The `<functional>` module of the Standard Library therefore defines a series of function object class templates, one for every built-in operator you may want to pass to other templates. The class template `std::less<>`, for instance, is fundamentally analogous to the Less template of Ex19_03. After adding an import for the `<functional>` module, you could thus replace the definition of the less variable in Ex19_03 with this one:

```
```cpp
std::less<int> less;    // Create a 'less than' functor
```
```

> **Tip**  As of C++14 the recommended way to use the function object types of the `<functional>` module is actually by omitting the type argument, for instance, as follows:

```
```cpp
std::less<> less;       // Create a 'less than' functor
```
```

The templates defined by `<functional>` employ more advanced template programming techniques to ensure that functors defined without an explicit type argument generally behave precisely like those defined the traditional way, except in specific situations that involve implicit conversions. The function object type `std::less<>` may lead to more efficient code than a function object of type `std::less<int>` (or, to use a