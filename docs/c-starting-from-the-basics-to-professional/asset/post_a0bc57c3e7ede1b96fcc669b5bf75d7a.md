
```cpp
    std::cout << "The largest of numbers is " << largest(numbers) << std::endl;
    std::cout << "The largest of data is " << largest(data) << std::endl;
    std::cout << "The largest of names is " << largest(names) << std::endl;
}

// Finds the largest of an array of double values
double largest(const double data[], size_t count)
{
    double max{ data[0] };
    for (size_t i{ 1 }; i < count; ++i)
        if (max < data[i]) max = data[i];
    return max;
}

// Finds the largest of a vector of double values
double largest(const std::vector<double>& data)
{
    double max {data[0]};
    for (auto value : data)
        if (max < value) max = value;
    return max;
}

// Finds the largest of a vector of int values
int largest(const std::vector<int>& data)
{
    int max {data[0]};
    for (auto value : data)
        if (max < value) max = value;
    return max;
}

// Finds the largest of a vector of string objects
std::string largest(const std::vector<std::string>& words)
{
    std::string max_word {words[0]};
    for (const auto& word : words)
        if (max_word < word) max_word = word;
    return max_word;
}
```

This produces the following output:

```text
The largest of array is 44.6
The largest of numbers is 44
The largest of data is 8.7
The largest of names is Jane Austen
```

The compiler selects the version of `largest()` to be called in `main()` based on the argument list. Each version of the function has a unique signature because the parameter lists are different. It’s important to note that the parameters that accept `vector<T>` arguments are references. If they are not specified as references, the vector object will be passed by value and thus copied. This could be expensive for a vector with a lot of elements. Parameters of array types are different. Only the address of an array is passed in this case, so they do not need to be reference types.

> **Note**  Did it bother you that several of the `largest()` functions in Ex8_14.cpp had the exact same implementation, only for a different type? If so, good. A good programmer should always be wary of repeating the same code multiple times—and not just because programmers are a lazy bunch. Later we’ll call this code *duplication* and explain to you some other downsides of doing this beyond having to type a lot. To avoid this particular type of duplication—where multiple functions perform the same task but for different parameter types—you need function templates. You will learn about function templates in Chapter 10.

## Overloading and Pointer Parameters

Pointers to different types are different, so the following prototypes declare different overloaded functions:

```cpp
int largest(int* pValues, size_t count);   // Prototype 1
int largest(float* pValues, size_t count);  // Prototype 2
```

Note that a parameter of type `int*` is treated in the same way as a parameter type of `int []`. Hence, the following prototype declares the same function as Prototype 1 earlier:

```cpp
int largest(int values[], size_t count);   // Identical signature to prototype 1
```

With either parameter type, the argument is an address and therefore not differentiated. In fact, you might recall from earlier that even the following prototype declares the same function:

```cpp
int largest(int values[100], size_t count);   // Identical signature to prototype 1
```

Because such array dimension specifications are completely ignored by the compiler, we argued earlier that they are thus dangerously misleading and advised you to never use this form. If a dimension specification is what you want, the recommended approach instead is either to use `std::array<>` or to pass arrays by reference.

## Overloading and Reference Parameters

You need to be careful when you are overloading functions with reference parameters. You can’t overload a function with a parameter type `data_type` with a function that has a parameter type `data_type&`. The compiler cannot determine which function you want from the argument. These prototypes illustrate the problem:

```cpp
void do_it(std::string number);    // These are not distinguishable...
void do_it(std::string& number);   // ...from the argument type
```

CHAPTER 8 | DEFINING FUNCTIONS

Suppose you write the following statements:

```cpp
std::string word {"egg"};

do_it(word);                 // Calls which???
```

The second statement could call either function. The compiler cannot determine which version of `do_it()` should be called. Thus, you can't distinguish overloaded functions based on a parameter for one version being of a given type and the other being a reference to that type.

You should also be wary when you have overloaded a function where one version has a parameter of type `type1` and another has a parameter reference to `type2`—even if `type1` and `type2` are different. Which function is called depends on the sort of arguments you use, but you may get some surprising results. Let's explore this a little with an example:

```cpp
// Ex8_15.cpp
// Overloading a function with reference parameters
import <iostream>;
import <format>;

double larger(double a, double b);  // Non-reference parameters
long& larger(long& a, long& b);     // Reference parameters

int main()
{
    double a_double {1.5}, b_double {2.5};
    std::cout << std::format("The larger of double values {} and {} is {}\n",
                             a_double, b_double, larger(a_double, b_double));

    int a_int {15}, b_int {25};
    std::cout << std::format("The larger of int values {} and {} is {}\n",
                             a_int, b_int,
                             larger(static_cast<long>(a_int), static_cast<long>(b_int)));
}

// Returns the larger of two floating point values
double larger(double a, double b)
{
    std::cout << "double larger() called." << std::endl;
    return a > b ? a : b;
}

// Returns the larger of two long references
long& larger(long& a, long& b)
{
    std::cout << "long ref larger() called" << std::endl;
    return a > b ? a : b;
}
```

This produces the following output:

```text
double larger() called.
The larger of double values 1.5 and 2.5 is 2.5.
double larger() called.
The larger of int values 15 and 25 is 25.0
```

The third line of output may not be what you were anticipating. You might expect the second output statement in `main()` to call the version of `larger()` with `long&` parameters. This statement has called the version with double parameters—but why? What caused both arguments to be converted to long?

That is exactly where the problem lies. The arguments are not `a_int` and `b_int` but temporary locations that contain the same values after conversion to type `long`. As we explained earlier, the compiler will not use a temporary address to initialize a reference-to-non-const.

So, what can you do about this? You have a couple of choices. If `a_int` and `b_int` were type `long`, the compiler will call the version of `larger()` with parameters of type `long&`. If the variables can’t be type `long`, you could specify the parameters as references-to-const like this:

```cpp
long larger(const long& a, const long& b);
```

Clearly, you must change the function prototype too. The function works with either const or non-const arguments. The compiler knows that the function won’t modify the arguments, so it will call this version for arguments that are temporary values instead of the version with double parameters. Note that the return type is `long` now. If you insist on returning a reference, the return type must be `const` because the compiler cannot convert from a reference-to-const to a reference-to-non-const.

## Overloading and const Parameters

A `const` parameter is only distinguished from a non-`const` parameter for references and pointers. For a fundamental type such as `int`, for example, `const int` is identical to `int`. Hence, the following prototypes are not distinguishable:

```cpp
long larger(long a, long b);
long larger(const long a, const long b);
```

The compiler ignores the `const` attribute of the parameters in the second prototype. This is because the arguments are passed by value, meaning that a copy of each argument is passed into the function, and thus the original is protected from modification by the function. There is no point in specifying parameters as `const` in a function prototype when the arguments are passed by value.

Naturally, while it is pointless in a function prototype, in a function definition it can certainly make sense to declare parameter variables `const`. You can do this to prevent the function's local copies of the arguments from being modified, and you can even do this if some earlier function prototype did not contain the `const` specifiers. The following is therefore perfectly valid—and even quite sensible:

```cpp
// Function prototype
long larger(long a, long b);    // const specifiers would be pointless here

/* ... */
```
