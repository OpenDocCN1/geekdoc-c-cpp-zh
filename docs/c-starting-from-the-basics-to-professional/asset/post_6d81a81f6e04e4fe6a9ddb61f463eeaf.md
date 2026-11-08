
This basic functor class has only one member: a function call operator. The main thing to remember here is that the function call operator is denoted with operator() and that its actual parameter list is specified only after an initial set of empty parentheses. Beyond that, this is just like any other operator function.

With this class definition, you can create your very first function object and then call it as if it were an actual function like so:

```
Less less;                        // Create a 'less than' functor...
const bool is_less = less(5, 6);  // ... and 'call' it
std::cout << (is_less ? "5 is less than 6" : "Huh?") << std::endl;
```

Of course, what is being "called" is not the object but rather its function call operator function. If you're into self-harm and code-obscuring, you could also write less(5, 6) as less.operator()(5, 6).

Granted, creating a functor just to call it right after is not very useful at all. Things become a bit more interesting already if you use a functor as a callback function. To demonstrate this, you'll first have to generalize the findOptimum() template of Ex19_02 since currently it only accepts a function pointer for its callback argument. Of course, creating an extra overload specifically for the Less type would defeat the purpose of having a higher-order function with a callback in the first place. And there's also no such thing as one single type that encompasses all function object class types. The most common way to generalize a function such as findOptimum() is therefore to declare a second template type parameter and use it as the type of the compare parameter:

```
// Optimum.cpp - a function template to determine the optimum element in a given vector
export module optimum;
import <vector>;

export template <typename T, typename Comparison>
const T* findOptimum(const std::vector<T>& values, Comparison compare)
{
    if (values.empty()) return nullptr;

    const T* optimum = &values[0];
    for (size_t i {1}; i < values.size(); ++i)
    {
        if (compare(values[i], *optimum))
            optimum = &values[i];
    }
    return optimum;
}
```

Because Comparison is a template type parameter, you can now invoke findOptimum() with compare arguments of any type you like. Naturally, the template's instantiation will then only compile if the compare argument is a function-like value that can be called with two T& arguments. And you know of two categories of arguments that might fit this bill already:

- Function pointers of type bool (*)(const T&, const T&) (or similar types, such as for instance bool (*)(T, T)). Therefore, if you were to plug this new definition of findOptimum<>() into Ex19_02, this example would still work precisely like before.
- Function objects of a type like Less that have a corresponding function call operator.

Both options are demonstrated in our next example:

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
    Less less;

    std::vector numbers{ 91, 18, 92, 22, 13, 43 };
    std::cout << "Minimum element: " << *findOptimum(numbers, less) << std::endl;
    std::cout << "Maximum element: " << *findOptimum(numbers, greater<int>) << std::endl;
}
```

## Standard Function Objects

You can customize many templates of the Standard Library by providing them with a first-class function, similar to what you did with `findOptimum()` in examples Ex19_02 and Ex19_03. For regular functions you can mostly use a plain function pointer, but for built-in operators that is not an option. You cannot create a pointer to a built-in operator. Of course, it is easy to quickly define either a function (as in Ex19_02) or a functor class (Less in Ex19_03) that emulates the operator's behavior, but doing so for every operator all the time would become tedious very fast.

Of course, this did not escape the designers of the Standard Library either. The `<functional>` module of the Standard Library therefore defines a series of function object class templates, one for every built-in operator you may want to pass to other templates. The class template `std::less<>`, for instance, is fundamentally analogous to the Less template of Ex19_03. After adding an import for the `<functional>` module, you could thus replace the definition of the less variable in Ex19_03 with this one:

```cpp
std::less<int> less;    // Create a 'less than' functor
```

> **Tip** As of C++14 the recommended way to use the function object types of the `<functional>` module is actually by omitting the type argument, for instance, as follows:

```cpp
std::less<> less;       // Create a 'less than' functor
```

The templates defined by `<functional>` employ more advanced template programming techniques to ensure that functors defined without an explicit type argument generally behave precisely like those defined the traditional way, except in specific situations that involve implicit conversions. The function object type `std::less<>` may lead to more efficient code than a function object of type `std::less<int>` (or, to use a more common example, more efficient than, say, one of type `std::less<std::string>`). Explaining this in more detail would lead us too far astray, though. Trust us: If you simply always omit the type argument, you're guaranteed that the compiler can generate optimal code under all circumstances. Plus, it saves you some typing, so it's a clear win-win!

Table 19-1 lists the complete set of templates. As always, all these types are defined in the `std` namespace.

*Table 19-1. The Function Object Class Templates Offered by the `<functional>` Module*

| | |
|---|---|
| Comparisons | `less<>`, `greater<>`, `less_equal<>`, `greater_equal<>`, `equal_to<>`, `not_equal_to<>` |
| Arithmetic operations | `plus<>`, `minus<>`, `multiplies<>`, `divides<>`, `modulus<>`, `negate<>` |
| Logical operations | `logical_and<>`, `logical_or<>`, `logical_not<>` |
| Bitwise operations | `bit_and<>`, `bit_or<>`, `bit_xor<>`, `bit_not<>` |

We could use `std::greater<>` to replace our `greater<>` function template of Ex19_03. Now isn't that great?

```cpp
std::vector numbers{ 91, 18, 92, 22, 13, 43 };
std::cout << "Minimum element: " << *findOptimum(numbers, std::less<>) << std::endl;
std::cout << "Maximum element: " << *findOptimum(numbers, std::greater<>) << std::endl;
```

This time we created the `std::less<>` and `std::greater<>` function objects as temporary objects directly inside the function call expression itself, rather than storing them first in a named variable. You can find this variant of the program in Ex19_03A.

## Parameterized Function Objects

Perhaps you've already noticed that, in fact, none of the function objects that you have seen thus far has been more powerful than a plain function pointer. Why go through all the trouble of defining a class with a function call operator if defining a plain function is so much easier? Surely, there must be more to function objects than this?

Indeed there is. Function objects only truly become interesting once you start adding more members—either variables or functions. Building on the same `findOptimum()` example as always, suppose you want to search for not the smallest or largest number but instead for the number that is nearest to some user-provided value. There is no clean way for you to accomplish this using functions and pointers to functions. Think about it: how would the callback's function body ever get access to the value that the user has entered? There is no clean way for you to pass this value along to the function if all you have is a pointer. If you use a function-like object, however, you can pass along any information you want by storing it in the object's member variables. The easiest is if we just show you how you might do this:

```cpp
// Nearer.cpp
// A class of function objects that compare two values based on how close they are
// to some third value that was provided to the functor at construction time.
module;             // Global module fragment to include legacy C headers (see Chapter 11)
```
