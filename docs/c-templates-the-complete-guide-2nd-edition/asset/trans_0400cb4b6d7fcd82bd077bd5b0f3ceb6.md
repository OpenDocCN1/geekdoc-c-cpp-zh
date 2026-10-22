
```
if constexpr (std::is_lvalue_reference<decltype((e))>::value) {
    std::cout << "expression is lvalue\n";
}
else if constexpr (std::is_rvalue_reference<decltype((e))>::value) {
    std::cout << "expression is xvalue\n";
}
else {
    std::cout << "expression is prvalue\n";
}
```

```
void display_num(int);    // #1
void display_num(double);  // #2

int main()
{
    display_num(399);      // #1 matches better than #2
    display_num(3.99);     // #2 matches better than #1
}
```

```
void combine(int, double);
void combine(long, int);

int main()
{
    combine(1, 2);  // ambiguous!
}
```

```
int f1(int);      // #1
int f1(double);   // #2
f1(4);            // calls #1: perfect match (#2 requires a standard conversion)

int f2(int);      // #3
int f2(char);     // #4
f2(true);         // calls #3: match with promotion
//                 (#4 requires stronger standard conversion)

class X {
    public:
        X(int);
};
int f3(X);        // #5
int f3(...);      // #6
f3(7);            // calls #5: match with user-defined conversion
//                 (#6 requires a match with ellipsis)
```

```
template<typename T>
class MyString {
  public:
    MyString(T const*);  // converting constructor
    ...
};

template<typename T>
MyString<T> truncate(MyString<T> const&, int);
int main()
{
    MyString<char> str1, str2;
    str1 = truncate<char>("Hello World", 5);    // OK
    str2 = truncate("Hello World", 5);          // ERROR
}
```

```
template<typename T> void strange(T&&, T&&);
template<typename T> void bizarre(T&&, double&&);

int main()
{
    strange(1.2, 3.4);  // OK: with T deduced to double
    double val = 1.2;
    strange(val, val);  // OK: with T deduced to double&
    strange(val, 3.4);  // ERROR: conflicting deductions
    bizarre(val, val);  // ERROR: lvalue val doesn't match double&&
}
```

```
#include <cstddef>

class BadString {
    public:
        BadString(char const*);
        ...

        // character access through subscripting:
        char& operator[] (std::size_t);                     // #1
        char const& operator[] (std::size_t) const;

        // implicit conversion to null-terminated byte string:
        operator char* ();                                  // #2
        operator char const* ();
        ...
};

int main()
{
    BadString str("correkt");
    str[5] = 'c';  // possibly an overload resolution ambiguity!
}
```

```
struct S {
    void f1();     // implicit *this parameter is an lvalue reference (see below)
    void f2() &&;  // implicit *this parameter is an rvalue reference
    void f3() &;   // implicit *this parameter is an lvalue reference
};
```

```
void report(int);      // #1
void report(int&);     // #2
void report(int const&); // #3

int main()
{
    for (int k = 0; k<10; ++k) {
        report(k);      // ambiguous: #1 and #2 match equally well
    }
    report(42);         // ambiguous: #1 and #3 match equally well
}
```

```
```cpp
class Base {
public:
    operator short() const;
};

class Derived : public Base {
};

void count(int);

void process(Derived const& object)
{
    count(object);    // matches with user-defined conversion
}
```
```

```
class Interface {
    ...
};

class CommonProcesses : public Interface {
    ...
};

class Machine : public CommonProcesses {
    ...
};

char* serialize(Interface*);        // #1
char* serialize(CommonProcesses*);  // #2

void dump (Machine* machine)
{
    char* buffer = serialize(machine);  // calls #2
    ...
}
```

overload/initlist.cpp

```
#include <initializer_list>
#include <string>
#include <vector>
#include <complex>
#include <iostream>

void f(std::initializer_list<int>) {
    std::cout << "#1\n";
}

void f(std::initializer_list<std::string>) {
    std::cout << "#2\n";
}

void g(std::vector<int> const& vec) {
    std::cout << "#3\n";
}
```

```
```cpp
void h(std::complex<double> const& cmplx) {
    std::cout << "#4\\n";
}

struct Point {
    int x, y;
};
void i(Point const& pt) {
    std::cout << "#5\\n";
}

int main()
{
    f({1, 2, 3});                       // prints #1
    f({"hello", "initializer", "list"}); // prints #2
    g({1, 1, 2, 3, 5});                  // prints #3
    h({1.5, 2.5});                      // prints #4
    i({1, 2});                           // prints #5
}
```
```

overload/initlistovl.cpp

```
#include <initializer_list>
#include <iostream>

void ovl(std::initializer_list<char>) {  //#1
    std::cout << "#1\n";
}

void ovl(std::initializer_list<int>) {  //#2
    std::cout << "#2\n";
}

int main()
{
    ovl({'h', 'e', 'l', 'l', 'o', '\0'});  // prints #1
    ovl({'h', 'e', 'l', 'l', 'o', 0});     // prints #2
}
```

overload/initlistctor.cpp

```
#include <initializer_list>
#include <string>
#include <iostream>

template<typename T>
struct Array {
    Array(std::initializer_list<T>) {
        std::cout << "#1\n";
    }
    Array(unsigned n, T const&) {
        std::cout << "#2\n";
    }
};
```

```
void arr1(Array<int>) {
}

void arr2(Array<std::string>) {
}

int main()
{
    arr1({1, 2, 3, 4, 5});          // prints #1
    arr1({1, 2});                  // prints #1
    arr1({10u, 5});                // prints #1
    arr2({"hello", "initializer", "list"});   // prints #1
    arr2({10, "hello"});         // prints #2
}
```

```
std::trait<...>::value
std::trait<...>()
std::trait_v<...>
```

> // 隐式转换为其类型
> // 自 C++17 起

# utils/traits1.cpp

```
```cpp
#include <type_traits>
#include <iostream>
int main()
{
    int i = 42;
    std::add_const<int>::type c = i;       // c is int const
    std::add_const_t<int> c14 = i;         // since C++14
    static_assert(std::is_const<decltype(c)>::value, "c should be const");

    std::cout << std::boolalpha;
    std::cout << std::is_same<decltype(c), int const>::value // true
              << '\n';
    std::cout << std::is_same_v<decltype(c), int const>       // since C++17
              << '\n';
    if (std::is_same<decltype(c), int const>{}) { // implicit conversion to bool
        std::cout << "same \n";
    }
}
```
```

```
namespace std {
    template<typename T, T val>
    struct integral_constant {
        static constexpr T value = val;                     // value of the trait
        using value_type           = T;                     // type of the value
        using type                 = integral_constant<T,val>;
        constexpr operator value_type() const noexcept {
            return value;
        }
        constexpr value_type operator() () const noexcept { // since C++14
            return value;
        }
    };
}
```

utils/traits2.cpp

```
#include <type_traits>
#include <iostream>

int main()
{
    using namespace std;
    cout << boolalpha;

    using MyType = int;
    cout << is_const<MyType>::value << '\n';  // prints false

    using VT = is_const<MyType>::value_type;  // bool
    using T = is_const<MyType>::type;         // integral_constant<bool, false>
    cout << is_same<VT,bool>::value << '\n';  // prints true
    cout << is_same<T, integral_constant<bool, false>>::value
         << '\n';                             // prints true
    cout << is_same<T, bool_constant<false>>::value
         << '\n';                             // prints true (not valid
                                             // prior to C++17)
```

```
```cpp
auto ic = is_const<MyType>();                         // object of trait type
cout << is_same<decltype(ic), is_const<int>>::value << '\n';  // true
cout << ic() << '\n';                                  // function call (prints false)

static constexpr auto mytypeIsConst = is_const<MyType>{};
if constexpr(mytypeIsConst) {             // compile-time check since C++17 => false
    ...                                     // discarded statement
}
static_assert(!std::is_const<MyType>{}, "MyType should not be const");
}
```
```
