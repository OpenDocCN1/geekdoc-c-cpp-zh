
< Less than

<= Less or equal to

>, >= Greater than and greater or equal to

[] Index operator

<< Output

>> Input

These operators eliminate the need for calls to functions such as strcpy and strcat.

# String Concatenation

The + operator can be used to concatenate a string object with another string object with a C-style string.

```
// A string demonstration
#include <iostream>
#include <string>
using namespace std;
int main() {
    string str1("Alpha");
    string str2("Beta");
    string str3("Omega");
    string str4;
    // assign a string
    str4 = str1;
    cout << str1 << "\n" << str4 << "\n";

    // concatenate two strings
    str4 = str1 + str2;
    cout << str4 << "\n";

    // concatenate a string with a C-string
    str4 = str1 + " " + str3;
    cout << str4 << "\n";

    // compare strings
    if(str3 > str1) cout << str3 > str1 << "\n";

    if(str3 == str1 + str2)
    cout << "str3 == str1+str2\n";
}

// Assign a C-style string to a string object
str1 = "This is a null-terminated string: ";

// copy constructed string object
str5(str1);
cout << str5 << endl;

// input and output a string
cout << "Enter a string: ";
cin >> str5;
cout << str5 << endl;
```

A string object is automatically sized to hold the string that it encapsulates. Thus, when assigning or concatenating strings, the target string will grow or shrink as needed to accommodate the size of the new string. It is not possible to have a buffer overflow for a string object.

# Convert A String Object To A C-Style String

The member function c_str() converts a string object to a null terminated C-style string:

```cpp
#include <iostream>
#include <cstring>
#include <string>

int main () {
    std::string str("hello world");

    const char* cstr = str.c_str();

    // cstr now contains a c-style string copy of str; including
    // the terminating null char
}
```

# STL Algorithms For Strings

The string class meets all of the basic requirements required for a container. Thus, it supports most common container functions, such as *begin, end, size* etc. It also supports iterators. A string object can also be manipulated by the STL algorithms.

# Modern C++ Type_Traits (C++11)

Type traits are a template meta-programming technique that lets us determine the type properties of variables at compile-time. Since the type information is obtained at compile-time there is zero run-time cost.

The C++ standard library implements a large number of predefined type traits that are defined in the <type_traits> header file.

A type trait is a struct that contains a single constant static data member. This member is named value if it answers a question about a type. The member is named type if it transforms a type.

Consider the following type trait declaration:

```cpp
#include <type_traits>
template<typename T>
struct is_floating_point;
```

This trait asks the question whether T is a floating point type or not. The struct answers this question. The struct is_floating_point contains a single static constant variable value. value is either true or false.

Suppose that we want to determine if a given type is a floating point type. The following code sample shows how this is done:

```cpp
#include <iostream>
#include <type_traits>
using namespace std;

class Foo {};

int main() {
	cout << is_floating_point<Foo>::value << '\n';
	cout << is_floating_point<float>::value << '\n';
	cout << is_floating_point<int>::value << '\n';
}
// output
```

In order to evaluate the previous expressions, the compiler generates the following
explicit structs and static constant values at compile-time:

```cpp
struct is_floating_point_Foo {
    static const bool value = false;
};

struct is_floating_point_float {
    static const bool value = true;
};

struct is_floating_point_int {
    static const bool value = false;
};
```

**Note:** const static data members of a class or struct can be initialized by assignment as
indicated above.

Since the struct data member value is a static constant, we can access it through the
scope operator as follows:

```cpp
std::is_floating_point<Foo>::value
```

# Modern C++: Automatic Type Inference (C++11)

Prior to C++11, the type of each program variable had to be explicitly specified in the variable's declaration. Since C++11 we can ask the compiler to deduce the type of a variable for us. C++11 has two new keywords for automatic type deduction: auto and decltype.

In C++11, we can declare a variable without specifying its type by setting the type of the variable to auto.

```cpp
auto i = 42; // i has type int
```

The auto type declaration, instructs the compiler to deduce the type of i at compile time. Because of type inference, we can replace a statement as int i = 42, with the statement auto i = 42;

Here is a more complex example where auto is used to simplify a type declaration:

```cpp
std::vector<int> vec;
std::vector<int>::iterator itr;
itr = vec.begin();
```

Instead of this we can use the simpler declaration:

```cpp
std::vector<int> vec;
auto itr = vec.begin();
```

The compiler will automatically deduce itr to have type: std::vector<int>::iterator.

Take a look at the following function template:

```cpp
template <typename BuiltType, typename Builder>
  BuiltType
  createObject(const Builder& builder) {
    return builder.makeObject();
}
```

This function template has two template parameters: one for the type of the Builder object, and a second for the type of the object that is built. Since the type of the built object cannot be deduced from the template parameter builder, we have to do an explicit specialization for each type of builder and the body of each function will specify the BuiltType that is returned by the function makeObject. This makes the template definition virtually useless.

But with auto we can deduce the return type of builder.makeObject(). This permits us to simplify the function template:

```cpp
template <typename Builder>
auto
createObject(const Builder& builder)
{
    return builder.makeObject();
}
```

# Modern C++: Type Deduction With decltype (C++11)

The decltype function returns a type. decltype has a variable or expression as it:

```cpp
int x = 3;
decltype(x) y;      // same as int y;
```

In this example, decltype(x) returns type int.

We can use decltype with any expression including a function declaration. In
particular, we can use decltype to declare the return type of a function or method.

For example, here is a use of decltype in a function template:

```cpp
template <typename Builder>
auto
createObject(const Builder& builder) -> decltype(builder.makeObject())
{
    auto val = builder.makeObject();

    return val;
}
```

# Type Attributes With Auto And decltype

Look at the following example:

```cpp
int &foo();              // function returns a reference
auto bar = foo();
```

The function foo returns a reference to an int. Bar is an int type or a reference to an
type? The answer is an int type, since auto does not preserve attributes such as const,

volatile or reference. (If we want to return a reference with auto&)

The decltype(...) type-specifier deduces a type like auto does. However, decltype deduces return types while preserving attributes such as reference, const and volatile.

# Modern C++: Trailing Return Types (C++11)

C++11 introduces a new syntax for the return type of a function. This syntax is called a trailing return type.

The syntax for trailing return types is:

```cpp
auto getSum() -> float;
```

The declaration auto getSum() -> float is equivalent to:

```cpp
float getSum();
```

When we use a trailing return type, the function declaration must start with auto. The type of the return value is deduced from the trailing return type and not auto.

One of trailing return types occurs in function templates where the return type of the function depends on the types of the arguments:

```cpp
#include <iostream>
template<class T, class U>
auto multiply(T lhs, U rhs) -> decltype(lhs * rhs)
{
    return lhs * rhs;
}
int main()
{
    auto value = multiply(2.3, 6);
    std::cout << value << std::endl;
}
// output
13.8
```
