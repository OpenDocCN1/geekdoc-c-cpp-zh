
```cpp
void Sandwich::SetBreadType(const wchar_t* breadType)
{
    m_pImpl->SetBreadType(breadType);
}

const wchar_t* Sandwich::GetSandwich(void)
{
    return m_pImpl->GetSandwich();
}
```

### Sample: `PimplSample\PimplSample.cpp`

```cpp
#include <iostream>
#include <ostream>

#include "Sandwich.h"
#include "../pchar.h"

using namespace std;

int _pmain(int /*argc*/, _pchar* /*argv*/[])
{
    Sandwich s;
    s.AddingIngredient(L"Turkey");
    s.AddingIngredient(L"Cheddar");
    s.AddingIngredient(L"Lettuce");
    s.AddingIngredient(L"Tomato");
    s.AddingIngredient(L"Mayo");
    s.RemoveIngredient(L"Cheddar");
    s.SetBreadType(L"a Roll");

    wcout << s.GetSandwich() << endl;

    return 0;
}
```

### Sample: `TemplatesSample\SimpleMath.h`

```cpp
#pragma once
template<class T>
class SimpleMath
{
public:

    SimpleMath(void) { }

    ~SimpleMath(void) { }

    T Add(T a, T b)
    {
        return a + b;
    }

    T Subtract(T a, T b)
    {
        return a - b;
    }

    T Multiply(T a, T b)
    {
        return a * b;
    }

    T Divide(T a, T b)
    {
        return a / b;
    }
};
```

As the name implies, this class is not meant to be more than a demonstration. There is only one type argument. Looking at the class definition, we can deduce that the requirements for T in this case are that it has the following operators, all of which operate on two instances of T and return an instance of T:

- `+`
- `-`
- `*`
- `/`

While these logically belong with numbers, you can define these operators for any class or data type and then instantiate an instance of this template class, which is specialized for your custom class (e.g., a Matrix class).

One last note, if you were to define the member functions outside of the class definition, but still inside the same header file, of course, then you would need to use the inline keyword in the declarations; the definitions would look like this: `SimpleMath<T>::SimpleMath(void) { }`.

This is the last file of this sample, showing a simple usage of each of the preceding templates.

### Sample: `TemplatesSample\TemplatesSample.cpp`

```cpp
#include <iostream>
#include <ostream>
#include <vector>
#include "SimpleMath.h"
#include "PeekLastItem.h"
#include "../pchar.h"

using namespace std;

int _pmain(int /*argc*/, _pchar* /*argv*/[])
{
    SimpleMath<float> smf;

    wcout << L"1.1F + 2.02F = " << smf.Add (1.1F, 2.02F) << L"F." <<
        endl;

    vector<const wchar_t*> strs;
    strs.push_back(L"Hello");
    strs.push_back(L"World");

    wcout << L"Last word was " <<
        PeekLastItem<std::vector<const wchar_t*,const wchar_t*> >(strs) <<
        L"." << endl;

    return 0;
}
```

## Chapter 12 Lambda Expressions

### No-Capture Lambdas

I assume that you have experience with lambdas from C#, so what we will do here is cover the syntax that C++ has adopted. All code snippets are from the same file in the same sample.

### Sample: `LambdaSample\LambdaSample.cpp`

```cpp
// Create a lambda-expression closure.
auto lm1 = []()
{
    wcout << L"No capture, parameterless lambda." << endl;
};

// Invoke the lambda.
lm1();
```

### Lambdas with Parameters

```cpp
// Create a lambda closure with parameters.
auto lm2 = [](int a, int b)
{
    wcout << a << L" + " << b << L" = " << (a + b) << endl;
};

lm2(3,4);
```

### Specifying a Lambda’s Return Type

The trailing return type here is -> int after the parameter specification.

```cpp
// Create a lambda closure with a trailing return type.
auto lm3 = [](int a, int b) -> int
{
    wcout << a << L" % " << b << L" = ";
    return a % b;
};

wcout << lm3(7, 5) << endl;
```

### Capturing Outside Variables

```cpp
int a = 5;
int b = 6;
// Capture by copy all variables that are currently in the scope.
// Note also that we do not need to capture the closure;
// here we simply invoke the anonymous lambda with the
// () after the closing brace.
[=]()
{
    wcout << a << L" + " << b << L" = " << (a + b) << endl;
    /// It's illegal to modify a here because we have
    /// captured by value and have not specified that
    /// this lambda should be treated as mutable.
    //a = 10;
}();

[=]() mutable -> void
{
    wcout << a << L" + " << b << L" = " << (a + b) << endl;
    // By marking this lambda as mutable, we can now modify a.
    // Since we are capturing by value, the modifications
    // will not propagate outside.
    a = 10;
}();

wcout << L"The value of a is " << a << L"." << endl;

[&]()
{
    wcout << a << L" + " << b << L" = " << (a + b) << endl;
    // By capturing by reference, we now do not need
    // to mark this as mutable.
    // Because it is a reference, though, changes now
    // propagate out.
    a = 10;
}();

wcout << L"The value of a is " << a << L"." << endl;

// Here we specify explicitly that we are capturing a by
// value and b as a reference.
[a,&b]()
{
    b = 12;
    wcout << a << L" + " << b << L" = " << (a + b) << endl;
}();

// Here we specify explicitly that we are capturing b as
// a reference and that all other captures should be by
// value.
[=,&b]()
{
    b = 15;
    wcout << a << L" + " << b << L" = " << (a + b) << endl;
}();

// Here we specify explicitly that we are capturing a by
// value and that all other captures should be by reference.
[&,a]()
{
    b = 18;
    wcout << a << L" + " << b << L" = " << (a + b) << endl;
}();
```

### Lambdas in Class-Member Functions

When you use a lambda in a class-member function, you cannot use a default capture by reference. This is because the lambda will be provided with a `this` pointer, and it must be copied. Also, when dealing with reference-counted smart pointers, it's common to run into problems with the lambda holding a reference to the class. Usually you will never get back to a reference count of zero, causing a memory leak in your program.

## Chapter 13 C++ Standard Library

### Introduction

There are far more things in the C++ Standard Library than we have time to cover. We will limit ourselves to looking at some of the most commonly used features that we haven’t yet explored.

### Iterators

Iterators serve the same purpose as IEnumerable and related interfaces in .NET, such as providing a common way to navigate through collections. Given a `std::vector`, for example, you can loop through its collection of items using the following code:

```cpp
vector<int> vec;
vec.push_back(1);
vec.push_back(4);
vec.push_back(7);
vec.push_back(12);
vec.push_back(8);

for (auto i = begin(vec); i != end(vec); i++)
{
    wcout << *i << endl;
}
```

The `std::begin` function provides an iterator pointing to the first item of the collection. `std::end` provides an iterator that signals we have reached the end of a collection; the last item of the collection, assuming the collection has any items, is one item before the item we are given by `std::end`. That’s why we check for `!=` in the `for` loop. If no items are in the collection, then `std::begin` and `std::end` will return the same value.

In addition to the iterators from those two template functions, many collections provide iterators via member functions named `cbegin` and `cend`, reverse iterators (that loop through a collection backwards) via `rbegin` and `rend`, and const reverse iterators via `crbegin` and `crend`. In the previous example, you can replace `begin(vec)` with `vec.rbegin()` and `end(vec)` with `vec.rend()` to go through the vector in reverse.

### Range-Based for Loops

C++11 has added an additional type of for loop, called the range-based for loop, which provides functionality similar to the `foreach` loop in C#. The range-based for loop uses iterators and provides you the trouble of de-referencing pointers and the possibility of improperly checking for the end. The range-based for loop equivalent to the for loop in the previous example looks like this:

```cpp
for (auto item : vec)
{
    wcout << item << endl;
}
```
