
```cpp
catch (...)
{
    // Handles all exceptions and does not rethrow...
}
```

The `noexcept` specifier may be used on all functions, including member functions, constructors, and destructors. You will encounter concrete examples later in this chapter.

In later chapters, you’ll even encounter several types of functions that should always be declared as `noexcept`. This includes `swap()` functions (discussed in Chapter 17) and move members (discussed in Chapter 18).

> **Note**  Unlike for instance in Java, in C++ you cannot specify what types of exceptions a non-`noexcept` function may throw. You used to be able to do so by appending `throw(exception_type1, ..., exception_typeN)` to a function header, but this feature has been removed from the language.

## Exceptions and Destructors

Starting with C++11, destructors are normally implicitly `noexcept`. Even if you define a destructor without a `noexcept` specification, the compiler will normally add one implicitly. This means that should the destructor of the following class be executed, the exception will never leave the destructor. Instead, `std::terminate()` shall always be called (in accordance with the implicit `noexcept` specifier added by the compiler):

```cpp
class MyClass
{
public:
    ~MyClass() { throw BigTrouble{}; }
};
```

It is in principle possible to define a destructor from which exceptions may be thrown. You could do so by adding an explicit `noexcept(false)` specification. But since you should normally never do this, we won’t discuss or consider this possibility any further.

> **Tip**  Never allow an exception to leave a destructor. All destructors are normally³ `noexcept`, even if not specified as such explicitly, so any exception they throw will trigger a call to `std::terminate()`.

## Exceptions and Resource Leaks

Making sure all exceptions are caught prevents catastrophic program failure. And catching them with properly positioned and sufficiently fine-grained catch blocks allows you to properly handle all errors. The result is a program that, at all times, either presents the desired result or can inform the user precisely what went wrong. But this is not the end of the story! A program that appears to be functioning robustly from the outside may still contain hidden defects. Consider, for instance, the following example program (it uses the same troubles module as Ex16_06):

```cpp
// Ex16_07.cpp
// Exceptions may result in resource leaks!
import <iostream>;
import troubles;
#include <cmath>    // For std::sqrt()

double computeValue(size_t x);            // A function to compute a single value
double* computeValues(size_t howMany);    // A function to compute an array of values

int main()
{
    try
    {
        double* values{ computeValues(10'000) };
        // Unfortunately we won't be making it this far...
        delete[] values;
    }
    catch (const Trouble&)
    {
        std::cout << "No worries: I've caught it!" << std::endl;
    }
}

double* computeValues(size_t howMany)
{
    double* values{ new double[howMany] };
    for (size_t i{}; i < howMany; ++i)
        values[i] = computeValue(i);
    return values;
}

double computeValue(size_t x)
{
    if (x < 100)
        return std::sqrt(x);    // Return the square root of the input argument
    else
        throw Trouble{"The trouble with trouble is, it starts out as fun!"};
}
```

If you run this program, a Trouble exception is thrown as soon as the loop counter in computeValues() reaches 100. Because the exception is caught in main(), the program does not crash. It even reassures the user that all is well. If this was a real program, you could even inform the user about what exactly went wrong with this operation and allow the user to continue. But that does not mean you are out of the woods! Can you spot what else has gone wrong with this program?

The computeValues() function allocates an array of double values in the free store, attempts to fill them, and then returns the array to its caller. It is the responsibility of the caller—in this case main()—to deallocate this memory. However, because an exception is thrown halfway through the execution of computeValues(), its values array is never actually returned to main(). Therefore, the array is never deallocated either. In other words, we have just leaked an array of 10,000 doubles!

Assuming computeValue() inherently leads to the occasional Trouble exception, the only place where we can fix this leak is in the computeValues() function. After all, main() never even receives a pointer to the leaked memory, so there is little that can be done about it there. In the spirit of this chapter thus far, a first obvious solution would therefore be to add a try block to computeValues() as follows (you can find this solution in Ex16_07A):

```cpp
double* computeValues(size_t howMany)
{
    double* values{ new double[howMany] };
    try
    {
        for (size_t i {0}; i < howMany; ++i)
            values[i] = computeValue(i);
        return values;
    }
    catch (const Trouble&)
    {
        std::cout << "I sense trouble... Freeing memory..." << std::endl;
        delete[] values;
        throw;
    }
}
```

Notice that values has to be defined outside the try block. Otherwise, the variable would be local to the try block, and we could not refer to it anymore from within the catch block. If you redefine computeValues() like this, no further changes are required to the rest of the program. It will also still have a similar outcome, except that this time the values array is not leaked:

```text
I sense trouble... Freeing memory...
No worries: I've caught it!
```

While this computeValues() with the try block makes for a perfectly correct program, it is not the most recommended approach. The function's code has become about twice as long and about twice as complicated as well. The next section introduces better solutions that do not suffer these shortcomings.

## Resource Acquisition Is Initialization

One of the hallmarks of modern C++ is the so-called RAII idiom, short for “resource acquisition is initialization.” Its premise is that each time you acquire a resource you should do so by initializing an object. Memory in the free store is a resource, but other examples include file handles (while holding these, other processes often may not access a file), mutexes (used for synchronization in concurrent programming), network connections, and so on. As per RAII, every such resource should be managed by an object, either

Nevertheless, there are of course Standard Library types that perform the same job as DoubleArrayRAII. In practice, you would therefore never write an RAII class to manage arrays.

A first such type is `std::unique_ptr<T[]>`. If you include the `<memory>` module, you can write `computeValues()` as follows:

```cpp
double* computeValues(size_t howMany)
{
    auto values{ std::make_unique<double[]>(howMany) };  // type unique_ptr<double[]>
    for (size_t i {}; i < howMany; ++i)
        values[i] = computeValue(i);
    return values.release();
}
```

In fact, with `std::unique_ptr<>`, an even better option would be to write it like this:

```cpp
std::unique_ptr<double[]> computeValues(size_t howMany)
{
    auto values { std::make_unique<double[]>(howMany) };
    for (size_t i {}; i < howMany; ++i)
        values[i] = computeValue(i);
    return values;
}
```

If you return the `unique_ptr<>` itself from `computeValues()`, you will of course have to slightly adjust the `main()` function accordingly. If you do, you'll notice that you no longer need the `delete[]` statement there. That's yet another potential source of memory leaks eliminated! Unless you are passing a resource to, for instance, a legacy function, there is rarely any need to release a resource from its RAII object. Just pass along the RAII object itself!

> **Note**  If you would attempt to return a `DoubleArrayRAII` object from `computeValues()` like this, you would run into a compiler error referring to its deleted copy constructor. To return a `DoubleArrayRAII` from a function you first need to enable move semantics for this class (as was done for, for instance, `std::unique_ptr<>`). We explain this further in Chapter 18.

Because the resource we are working with is a dynamic array, you of course know that you could simply use a `std::vector<>` instead as well:

```cpp
std::vector<double> computeValues(size_t howMany)
{
    std::vector<double> values;
    for (size_t i {}; i < howMany; ++i)
        values.push_back( computeValue(i) );
    return values;
}
```
