
Floating-point numbers and class-type objects are not allowed as nontype template parameters:

```cpp
template<typename T>
double precision Color<T> // not allowed as non-type parameter
{
    return v1;
}
```

```cpp
template<class T>
class MyClass // ERROR: class-type objects are not allowed as non-type template parameters
{
    // private parameters
};
```

When passing template arguments to pointers or references, the objects must not be string literals, temporaries, or data members and other sub-objects. Because these restrictions were relaxed with each and every C++ version before C++14, additional constraints apply:

- In C++11, the objects also had to have external linkage.
- In C++14, the objects also had to have external or internal linkage.

Thus, the following is not possible:

```cpp
template<char const* name>
class MyClass;

MyClass<"hello"> // ERROR: string literal "hello" not allowed
```

However there are workarounds (again depending on the C++ version):

```cpp
extern char const s03[] = "hi";   // external linkage
char const s11[] = "hi";          // internal linkage

int main()
{
    Messenger<s03> msg;             // for all versions
    Messenger<s11> msg;             // C++11 and C++14
    static char const s14[] = "hi"; // no linkage
    Messenger<s14> msg;             // C++17 and later
}
```

In all three cases a constant character array is initialized by "hello" and this object is used as a template parameter declared with either `const char*` or `const char[]`. This is valid in all C++ versions if the object has external linkage (s3), in C++11 and C++14 also if it has internal linkage (s11), and since C++17 if it has no linkage at all.

See Section 3.2.3 on page 157 for a detailed discussion and Section 7.2 on page 354 for a discussion of possible future changes in this area.

### Avoiding Invalid Expressions

Arguments for nontype template parameters might be any compile-time expressions. For example:

```cpp
template<int i, bool b>
class C;

C<sizeof(int) + 4, sizeof(int)> c;
```

However, note that if operator> is used in the expression, you have to put the whole expression into parentheses so that the nested > ends the argument list:

```cpp
C<42, sizeof(int) > 4> c;        // ERROR: first > ends the
                                 // template argument list
C<42, (sizeof(int) > 4)> c;      // OK
```

### 3.4 TEMPLATE PARAMETER TYPE AUTO

Internally you can use both the value:

```cpp
std::array<T,5>::size_type    // elements
```

and its type:

```cpp
using size_type = decltype(array.size());
```

which is then, for example, used as return type of the size() member function:

```cpp
size_type size() const   // return current number of elements
{
    return num_elements;
}
```

Since C++14, you could also just use auto here as return type to let the compiler find out the return type:

```cpp
auto size() const   // return current number of elements
{
    return num_elements;
}
```

With this class declaration the type of the number of elements is defined by the type used for the number of elements, when using a stack:

```cpp
basics/stackauto.cpp

#include <iostream>
#include <string>
#include "stackauto.hpp"

int main()
{
    Stack<int,20> int20Stack;          // stack of 20 ints
    Stack<std::string,40> stringStack; // stack of 40 strings

    // manipulate stack of up to 20 ints

    int20Stack.push(7);

    std::cout << int20Stack.top() << '\n';
    auto size1 = int20Stack.size();

    // manipulate stack of up to 40 strings

    stringStack.push("hello");

    std::cout << stringStack.top() << '\n';
    auto size2 = stringStack.size();

    if (std::is_same_v<decltype(size1), decltype(size2)>) {
        std::cout << "same type" << '\n';
    }
}
```

```cpp
Stack<int,20> int20Stack;        // stack of up to 20 ints
```

the internal size type is unsigned int, because 20 is passed.

With

```cpp
Stack<std::string,40> stringStack;  // stack of up to 40 strings
```

the internal size type is int, because 40 is passed.

The `size()` member functions for the two stacks will have different return types, in that when

```cpp
auto size2 = stringStack.size();
```

The types of `size1` and `size2` differ. By using the standard type trait `std::is_same` (see Section 13.3 on page 725) and `decltype`, we can check that:

```cpp
if (std::is_same<decltype(size1), decltype(size2)>::value) {
    std::cout << "same type" << '\n';
} else {
    std::cout << "size types differ" << '\n';
}
```

Thus, the output will be:

```text
size types differ
```

Since C++17, for traits returning values, you can also use the suffix `_v` instead of `::value` (see Section 5.6 on page 85 for details):

```cpp
if (std::is_same_v<decltype(size1), decltype(size2)>) {
    std::cout << "same type" << '\n';
}
```

Note that other constraints on the type of non-type template parameters remain in effect. Especially, the restrictions about possible types for non-type template arguments discussed in Section 3.3 on page 49 still apply. For example:

```cpp
Stack<int, 3.14>;    // ERROR: Floating-point non-type argument not allowed
```

And, because you can now allow strings as constant values (using static locally declared; see Section 3.5 on page 49), the following is possible:

```cpp
basicString<"heap.cpp">
```

```cpp
#include <iostream>

template<auto T>       // allow values of any possible type
class Message {
  public:
    void print() {
      std::cout << T << '\n';
    }
};

int main()
{
  Message<42> msg1;
  msg1.print();         // initialize with int 42 and print it

  static char const s[] = "hello";
  Message<s> msg2;      // initialize with char const[]
  msg2.print();         // and print that value
}
```

Note also that even `template<decltype(auto) N>` is possible, which allows instantiation of `N` as a reference:

```cpp
template<decltype(auto) N>
class C {
  // ...
};

int i;
C<i> x;    // N is int&
```

See Section 15.1.1 on page 926 for details.

### 3.5 SUMMARY

- Templates can have template parameters that are values rather than types.
- You cannot use floating-point numbers or class-type objects as arguments for non-type template parameters. For pointers/references to string literals, temporaries, and subobjects, restrictions apply.

## Chapter 4

## Variadic Templates

Since C++11, templates can have parameters that accept a variable number of parameters. This feature allows the use of templates in places where you have to pass an arbitrary number of arguments of arbitrary type. A typical application is to pass an arbitrary number of parameters of arbitrary type through a class or framework. Another application is to provide generic code to process any number of parameters of any type.

### 4.1 VARIADIC TEMPLATES

Template parameters can be defined to accept an unbounded number of template arguments. Templates with this ability are called variadic templates.

#### 4.1.1 Variadic Templates by Example

For example, you can use the following code to call `print()` for a variable number of arguments of different types:

```cpp
#include <iostream>

void print ()
{
}

template<typename T, typename... Types>
void print (T firstArg, Types... args)
{
    std::cout << firstArg << '\n';    // call print() for ...
    print(args...);
}
```

If one or more arguments are passed, the function template is used. The first argument is printed separately before recursively calling `print()` for the remaining arguments. To end the recursion, the `print()` function with no arguments is called.

```cpp
void print ()
{
}
```

using different types specified by a template parameter pack

```cpp
template<typename T, typename... Types>
```

To end the recursion, the non-template overload of `print()` is provided, which is used when the parameter pack is empty.

For example, a call such as

```cpp
std::string s ("world");
print (7.5, "hello", s);
```

would output the following:
