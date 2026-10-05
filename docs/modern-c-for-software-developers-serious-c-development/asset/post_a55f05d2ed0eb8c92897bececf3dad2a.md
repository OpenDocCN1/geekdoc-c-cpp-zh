
implicitly converted to an enum type by the compiler and an enum type will not
implicitly converted to an integer type. Thus the following program with a scoped
enum will not compile:

```cpp
#include <iostream>
#include <string>

int main()
{
    enum class Color { RED, GREEN, BLUE };
    Color my_color;

    my_color = 1;      // error
    if (my_color == Color::GREEN)
        std::cout << "green color" << std::endl;
}
```

// output
error: cannot convert 'int' to 'main()::Color' in assignment

This strong type safety also applies to unscoped enums in C++11.

## Forward References For Enums

We can specify forward declarations for scoped and unscoped enums:

- # forward declaration of Mood enum
enum class Mood;

## Well-defined Enum Sizes: `<cstdint>`

CC++ does not ordinarily provide fixed, well-defined bit sizes for it's native types. For
example, sometimes we want a 32 bit integer, not just an int type. This is because
int type might have different sizes on different CPU architectures. C++11 solves this
problem with the C99 header file std.h. We include this header file as #include

<cstdint> to specify integer types with well-defined sizes.

The cstdint header includes types such as std::int_t, std::int16_t, std::int32_t, and std::int64_t (as well as unsigned versions that begin with a u prefix). For example: std::uint8_t refers to an unsigned int type that is 8 bits long. The integer types in the cstdint header specify the bit sizes of the various types.

We can use these cstdint types as follows:

```cpp
#include <cstdint>
enum class Colour : std::int8_t { RED = 1, GREEN = 2, BLUE = 3 };
```

## Modern C++: Type Alias (C++11)

### Typedef

A C or C++ typedef declaration introduces a name that, within its scope, becomes a synonym for an existing type. The syntax is:

```cpp
typedef [existing-type] [our-alias];
```

And here is an example:

```cpp
// Declare UL as a synonym for the unsigned long type.
typedef unsigned long UL;
UL x = 5;
```

### Type Alias Declarations With The using Keyword (using =)

We have previously seen that we can bring a namespace into scope with the using keyword:

```cpp
using namespace std;
```

In C++11, we can also utilize the using keyword to declare that a name is an alias for a previously declared type. The syntax is:

```cpp
using new_type_name = some_declared_type;
```

The new type name is a synonym for the existing type within the new type's scope.

Here are some examples:

```cpp
using iter_t = std::vector<int, std::string>::iterator;
using counter = long;
using Map = std::map<std::string, std::string>;
```

using Type aliases also work with function pointers, but they are more readable than the equivalent typedef:

```cpp
double adder(int x, double y) {
    double z = x + y;
    return z;
}

// declaration of type funcptr
using funcptr = double(*)(int, double);

// definition
funcptr f = adder;

this is equivalent to:
void (*)(int, double) f = adder;
```

typedef and using can be used to impart semantic content to types: 

```cpp
using velocity = long;
```

## Using And Templates

An advantage of type alias declarations over typedefs is that the latter cannot be used with templates.

The following is the syntax for template aliases:

```cpp
template<class T> using Vec = std::vector<T, MyAllocator<T>>;
Vec<int> vec;
```

Vec is an alias for a family of std::vector types.

We read this as Vec<T> is a typedef for std::vector<T, MyAllocator<T>>.

## Modern C++: User Defined Literals (C++11)

In C++ there are four types of literals: integer, floating point, char and string literals. Integer literals can have a suffix that indicates the data type of the literal. For example, 89075ul indicates an unsigned long integer literal.

With user defined literals we can define our own units of measurement. This is accomplished by specifying a literal value and attaching a custom suffix to this value. The suffix converts the value into suffix units. For example:

```cpp
#include <iostream>
using namespace std;

float operator ""_sections(long double x) { return x / 640; }
int main() {
    float result = 1055.44__sections;
    cout << result << endl;
}
// 1.64912
```

This example converts acres into sections. A section is 640 acres. An integer literal with a custom suffix such as sections is called a user defined literal. The declaration syntax for user defined literals uses operator functions as follows:

```cpp
long double operator ""_cm(long double x) { return x * 10; }
long double operator ""_ms(long double x) { return x * 1000; }
long double operator ""_mi(long double x) { return x * 100000; }
```

operator "" signifies that we are declaring a user defined literal. _cm, _ms and _mi are custom suffixes. These operators have a long double parameter. The parameter is multiplied by 10, 1000 or 100000 and this value is returned. The return value can be any integer or floating point type. Permissible parameter types for user defined literals are described below.

The above definitions allow us to convert meters to centimetres, millimetres and micrometers.

The program below shows how to use user-defined literals.

```cpp
#include <iostream>
using namespace std;

float operator ""fi(long double x) { return 3.5 * x; }

int main() {
    float res3 = 4.88__fi;

    cout << res3 << endl;
}

// output
17.08
```

The previous program performs the floating point literal conversion at run-time. We can shift the calculation to compile-time by using constexpr. For example:

```cpp
constexpr operator ""fi(long double x) { return 3.5 * x; }
```

## Restrictions On User Types

User defined literals can only be used with the following:

- int
- float
- double
- size_t
- long
- long double

## Naming Rules For User Literals

The first rule is that user defined suffixes must start with an underscore. The second rule is that user defined suffixes cannot start with a capital letter after the underscore. There must be no space between the underscore and the letter.

```cpp
// error
100_A;
// ok
100_a;
```

## Modern C++: Type Constants (C++14)

As we have seen, C++11 also allows template constants. We can declare and initialize a template constant as follows:

```cpp
template<typename T>
const T value = 10;
```

If T is integer, then value is 10. If T is float, then value is 10.0f. If T is double, then value is 10.0.

This can be used to define constant constants.

## Modern C++: Return Type Deduction (C++14)

### Return type for functions

C++14 implements automatic type deduction for return values:

```cpp
auto square(int n)
{
    return n * n;
}
```

The type of the return value of *square* is deduced to be an *int* by the compiler.

### Generic Lambdas (C++14)

In C++14 we can specify the type of the lambda parameters as auto. The compiler will deduce the type of the lambda parameters from the values that the lambda receives. This de-fact feature effectively makes a lambda into an anonymous template function:

```cpp
auto my_lambda = [](auto a, auto b) { return a * b; };
```

Here is an example:

```cpp
#include <iostream>
#include <typeinfo>

int main() {
    auto f = [](auto a, auto b) {
        std::cout << "type of parameter a: " << typeid(a).name() << std::endl;
        std::cout << "type of parameter b: " << typeid(b).name() << std::endl;
        return a + b;
    };
    auto ret = f(2, 986.546);

    std::cout << "type of lambda return value: " << typeid(ret).name() << std::endl;
}

// output
type of parameter a: i
type of parameter b: d
type of lambda return value: d
```

### Extended Capture In Lambdas

In C++14, variables that are captured in a lambda introducer can be initialized:

```cpp
#include <iostream>

int main() {
    int foo = 30;
    std::cout << foo << "foo before lambda = " << foo << std::endl;
}
```
