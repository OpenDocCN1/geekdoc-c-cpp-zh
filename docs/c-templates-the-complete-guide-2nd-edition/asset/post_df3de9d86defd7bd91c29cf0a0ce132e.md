
```
class C {
    public:
        template<typename T>
        C (T const&) {
            std::cout << "tmpl copy constructor\n";
        }
        ...
};
```

```
C x;
C y{x};  // still uses the predefined copy constructor (not the member template)
```

```
C x;
C y{x};  // uses the member template
```

```
template<typename T>
class C
{
    public:
        ...
        // user-define the predefined copy constructor as deleted
        // (with conversion to volatile to enable better matches)
        C(C const volatile&) = delete;

        // if T is no integral type, provide copy constructor template with better match:
        template<typename U,
                typename = std::enable_if_t<!std::is_integral<U>::value>>
        C (C<U> const&) {
            ...
        }
        ...
};
```

```
```cpp
template<typename T>
concept ConvertibleToString = std::is_convertible_v<T, std::string>;
```
```

```
template<typename STR>
requires ConvertibleToString<STR>
Person(STR&& n) : name(std::forward<STR>(n)) {
    ...
}
```

```
```cpp
template<ConvertibleToString STR>
Person(STR&& n) : name(std::forward<STR>(n)) {
    ...
}
```
```

```
template<typename T>
void printV (T arg) {
...
}
```

```
void printV (int arg) {
  ...
}
```

```
void printV (std::string arg)
{
    ...
}
```

```
std::string returnString();
std::string s = "hi";
printV(s);                  // copy constructor
printV(std::string("hi"));  // copying usually optimized away (if not, move constructor)
printV(returnString());      // copying usually optimized away (if not, move constructor)
printV(std::move(s));        // move constructor
```

```
template<typename T>
void printV (T arg) {
...
}
```

```
void printV (char const* arg)
{
  ...
}
```

```
template<typename T>
void printR (T const& arg) {
  ...
}
```

```
std::string returnString();
std::string s = "hi";
printR(s);                  // no copy
printR(std::string("hi"));  // no copy
printR(returnString());      // no copy
printR(std::move(s));        // no copy
```

```
int i = 42;
printR(i);    // passes reference instead of just copying i
```

```
template<typename T>
void printR (T const& arg) {
    ...
}

std::string const c = "hi";
printR(c);            //T deduced as std::string, arg is std::string const&

printR("hi");        //T deduced as char [3], arg is char const(&) [3]
int arr[4];
printR(arr);          //T deduced as int [4], arg is int const(&) [4]
```

```
template<typename T>
void outR (T& arg) {
  ...
}
```

```
std::string returnString();
std::string s = "hi";
outR(s);        // OK: T deduced as std::string, arg is std::string&
outR(std::string("hi"));  // ERROR: not allowed to pass a temporary (prvalue)
outR(returnString());       // ERROR: not allowed to pass a temporary (prvalue)
outR(std::move(s));         // ERROR: not allowed to pass an xvalue
```

```
template<typename T>
void outR (T& arg) {
    if (std::is_array<T>::value) {
        std::cout << "got array of " << std::extent<T>::value << " elems\n";
    }
    ...
}
```

```
std::string const c = "hi";
outR(c);                // OK: T deduced as std::string const
outR(returnConstString()); // OK: same if returnConstString() returns const string
outR(std::move(c));       // OK: T deduced as std::string const⁶
outR("hi");             // OK: T deduced as char const[3]
```

```
template<typename T>
requires !std::is_const_v<T>
void outR (T& arg) {
  ...
}
```

```
std::string s = "hi";
passR(s);                  // OK: T deduced as std::string& (also the type of arg)
passR(std::string("hi")); // OK: T deduced as std::string, arg is std::string&&
passR(returnString());     // OK: T deduced as std::string, arg is std::string&&
passR(std::move(s));       // OK: T deduced as std::string, arg is std::string&&
passR(arr);                // OK: T deduced as int(&) [4] (also the type of arg)
```

```
std::string const c = "hi";
passR(c);            // OK: T deduced as std::string const&
passR("hi");       // OK: T deduced as char const(&) [3] (also the type of arg)
int arr[4];
passR("hi");       // OK: T deduced as int (&) [4] (also the type of arg)
```

```
```cpp
template<typename T>
void passR(T&& arg) {  // arg is a forwarding reference
    T x;       // for passed lvalues, x is a reference, which requires an initializer
    ...
}

foo(42);   // OK: T deduced as int
int i;
foo(i);    // ERROR: T deduced as int&, which makes the declaration of x in passR() invalid
```
```

```
template<typename T>
void printT (T arg) {
  ...
}

std::string s = "hello";
printT(s);      // pass s by reference
printT(std::cref(s));   // pass s "as if by reference"
```

basics/cref.cpp

```
#include <functional> //for std::cref()
#include <string>
#include <iostream>

void printString(std::string const& s)
{
    std::cout << s << '\n';
}

template<typename T>
void printT (T arg)
{
    printString(arg);        // might convert arg back to std::string
}

int main()
{
    std::string s = "hello";
    printT(s);               // print s passed by value
    printT(std::cref(s));    // print s passed "as if by reference"
}
```

```
template<typename T>
void printV (T arg) {
    std::cout << arg << '\n';
}
...
std::string s = "hello";
printV(s);            // OK
printV(std::cref(s));   // ERROR: no operator << for reference wrapper defined
```

```
template<typename T1, typename T2>
bool isless(T1 arg1, T2 arg2)
{
    return arg1 < arg2;
}
...
std::string s = "hello";
if (isless(std::cref(s) < "world")) ...    // ERROR
if (isless(std::cref(s) < std::string("world"))) ...  // ERROR
```

```
template<typename T>
void foo (T const& arg1, T const& arg2)
{
...
}

foo("hi", "guy");  // ERROR
```

```
template<typename T>
void foo (T arg1, T arg2)
{
  ...
}

foo("hi", "guy");    // compiles, but...
```

```
```cpp
template<typename T>
void foo (T arg1, T arg2)
{
    if (arg1 == arg2) {  // OOPS: compares addresses of passed arrays
        ...
    }
}

foo("hi", "guy");       // compiles, but ...
```
```

```
```cpp
template<typename T, std::size_t L1, std::size_t L2>
void foo(T (&arg1)[L1], T (&arg2)[L2])
{
    T* pa = arg1;  // decay arg1
    T* pb = arg2;  // decay arg2
    if (compareArrays(pa, L1, pb, L2)) {
        ...
    }
}
```
```

```
template<typename T,
    typename = std::enable_if_t<std::is_array_v<T>>>
void foo (T&& arg1, T&& arg2)
{
    ...
}
```

```
```cpp
std::string* s = new std::string("whatever");
auto& c = (*s)[0];
delete s;
std::cout << c;    // run-time ERROR
```
```

```
auto s = std::make_shared<std::string>("whatever");
auto& c = (*s)[0];
s.reset();
std::cout << c;  // run-time ERROR
```

```
template<typename T>
T retR(T&& p)    //p is a forwarding reference
{
  return T{...};  // OOPS: returns by reference when called for lvalues
}
```

```
template<typename T>
typename std::remove_reference<T>::type retV(T p)
{
    return T{...};  // always returns by value
}
```

```
template<typename T>
auto retV(T p)  // by-value return type deduced by compiler
{
    return T{...};  // always returns by value
}
```

```
template<typename T1, typename T2>
pair<T1,T2> make_pair (T1 const& a, T2 const& b)
{
    return pair<T1,T2>(a,b);
}
```
