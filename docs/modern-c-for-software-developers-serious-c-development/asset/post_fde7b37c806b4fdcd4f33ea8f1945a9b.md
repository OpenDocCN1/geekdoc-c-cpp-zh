
```cpp
auto decrementor = [foo = 2] {
  std::cout << "foo value in lambda: " << foo << std::endl;
  return foo - 12;
};
```

```cpp
auto ret = decrementor();
std::cout << "foo value after lambda: " << foo << std::endl;
std::cout << "value returned by lambda = " << ret << std::endl;
```

```cpp
// output
foo before lambda: 30
foo value in lambda: 2
foo value after lambda: 30
value returned by lambda = -10
```

In this example the variable `foo` is passed by copy to the lambda. Since `foo` is a read-only variable, its value in the outer scope cannot be changed.

In the example that follows, a new variable is defined in the lambda introducer.

```cpp
#include <iostream>
int main() {
    auto decrementor = [foo = 2] { return foo - 12; };
    std::cout << decrementor() << std::endl;
}
```

```cpp
// output
-10
```

`foo` doesn't exist in the outer scope of the lambda, this is in effect a technique for adding data members to the lambda. A lambda variable in the introducer must be initialized if it does not exist in the outer scope of the lambda. A new lambda variable that is declared in an introducer is read only.

**Note:** The types of variables in a lambda introducer are not specified since they are inferred by the compiler either because the variable exists in the outer scope or because it is initialized in the lambda introducer.

# Modern C++: Constexpr Template Constants (C++14)

C++14 permits template constants to be `constexpr`. These constants are evaluated at compile-time.

```cpp
template<typename T>
constexpr T pi = T(3.14159265358979332385);
```

Note that `T(x)` is performing a C function-style type conversion of its parameter to type `T` (see function-style casts).

```cpp
#include <iostream>
template<typename T>
constexpr T pi = T(3.14159265358979332385);

template<typename T>
constexpr T area_of_circle(T radius)
{
    auto area = pi<T> * radius * radius;
    return area;
}

int main()
{
    auto area = area_of_circle(5.78);
    std::cout << area << std::endl;
}

// output
104.956
```

# Modern C++: Constexpr Functions (C++14)

C++14 allows more expressions inside the body of `constexpr` functions:

- local variable declarations are allowed inside constexpr functions provided they are not static or `thread_local` declarations. Local variables must be initialized.
- if, switch, for, while, do-while expressions are allowed inside constexpr functions.

# Modern C++: Binary Literals (C++14)

C++14 permits the declaration of binary literals. A binary literal begins with a `0B` or `0b` prefix that is followed by a sequence of 1's and 0's:

```cpp
auto y = 0b00000101; // integer 5 as a binary (base 2) literal
```

A binary literal has integral type.

# Modern C++: Digit Separator (C++14)

C++14 permits integer literals to be separated by apostrophes for better readability:

```cpp
12345'67890'1245LL
cout << 12345'67890'1245LL

std::cout << 0b1000'1110 << std::endl

std::cout << 0X12A'2b4 << std::endl
```

# Modern C++: [[deprecated]] Attribute (C++14)

The `[[deprecated]]` keyword warns a user that an expression, function, class or feature can be used but its usage is discouraged. The syntax is:

```cpp
[[deprecated]]
expression, function, class or enum that is deprecated
```

The compiler will emit a warning that the item is deprecated. An optional message can be attached by using the following syntax:

```cpp
[[deprecated("message")]]
```

Examples:

```cpp
// identifying the use of a deprecated function
[[deprecated("postgres sqlConnect function is obsolete")]]
int sqlConnect() {
```

```cpp
// identifying the use of a deprecated class
#include <iostream>
using namespace std;

int main() {
class [[ deprecated("Foo is obsolete") ]] Foo {
public:
  Foo() { cout << "in constructor" << endl; }
  int x;
};
Foo foo;
}
```

```cpp
// returns
warning: 'Foo' is deprecated: Foo is obsolete
```

# Modern C++: Template Type Deduction (C++17)

## Template Argument Type Deduction For Functions

Template argument type deduction refers to the compiler's ability to deduce the types of the arguments of a function template specialization.

In C++ argument type deduction for template functions is implemented as follows. Consider the following function template declaration:

```cpp
template<typename T>
void foo(const T& data)
```

In C++17, we can use class argument deduction (CTAD) to avoid specifying template arguments for classes.

# Modern C++: Template Type Deduction (C++17)

## Template Type Deduction For Classes

In C++17, we can use class argument deduction (CTAD) to avoid specifying template arguments for classes.

```cpp
template <typename A, typename B>
struct MyPair
{
  MyPair() {}
  MyPair(const A&, const B&) {}
};

int main()
{
  MyPair p1 {11, 22}; // Duces MyPair<int, int>
  // MyPair p2; // Error: no matching constructor
}
```

# Modern C++: Non-Template Type Parameters (C++17)

In C++11 and C++14 we can use the type `auto` whenever we can automatically deduce the types of template parameters or function return types. `auto` can also be used in generic lambdas.

Until C++17 the types of non-template parameters had to be explicitly declared in a class template or function template since the compiler would not deduce the types of these parameters.

## Summary Of Non Template-Type Parameters

The following is an example of using a parameter which is not a template type in a template:

```cpp
#include <iostream>
// size is a non-template type parameter
template<class T, int size>
class Foo
{
  T array[size];
public:
  Foo() {}
  -Foo() {};

  int getSize() const
  {
    return size;
  }
};

int main(){
  Foo<double, 29> foo;
  auto size = foo.getSize();
  std::cout << size << std::endl;
}

// output
29
```
