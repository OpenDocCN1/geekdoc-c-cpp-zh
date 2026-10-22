
```cpp
int main()
{
    std::vector<int> primes = { 2, 3, 5, 7, 11, 13, 17, 19 };

    foreach(primes.begin(), primes.end(),  // range
            func);                         // function as callable (decays to pointer)

    foreach(primes.begin(), primes.end(),  // range
            &func);                        // function pointer as callable

    foreach(primes.begin(), primes.end(),  // range
            FuncObj());                    // function object as callable

    foreach(primes.begin(), primes.end(),  // range
            [] (int i) {                   // lambda as callable
        std::cout << "lambda called for: " << i << '\n';
    });
}
```

op.operator()(*current);  // call operator() with parameter *current for op

basics/foreachinvoke.hpp

```cpp
#include <utility>
#include <functional>

template<typename Iter, typename Callable, typename... Args>
void foreach (Iter current, Iter end, Callable op, Args const&... args)
{
    while (current != end) {    // as long as not reached the end of the elements
        std::invoke(op,           // call passed callable with
                    args...,      // any additional args
                    *current);    // and the current element
        ++current;
    }
}
```

```
// pass lambda as callable and an additional argument:
foreach(primes.begin(), primes.end(),          // elements for 2nd arg of lambda
    [](std::string const& prefix, int i) { // lambda to call
        std::cout << prefix << i << '\n';
    },
    "- value: ");
                                        // 1st arg of lambda

// call obj.memfunc() for/with each elements in primes passed as argument
MyClass obj;
foreach(primes.begin(), primes.end(),  // elements used as args
    &MyClass::memfunc,                 // member function to call
    obj);                              // object to call memfunc() for
}
```

basics/invoke.hpp

```cpp
#include <utility>    // for std::invoke()
#include <functional> // for std::forward()

template<typename Callable, typename... Args>
decltype(auto) call(Callable&& op, Args&&... args)
{
    return std::invoke(std::forward<Callable>(op),    // passed callable with
                       std::forward<Args>(args)...); // any additional args
}
```

```cpp
template<typename Callable, typename... Args>
decltype(auto) call(Callable&& op, Args&&... args)
```

```cpp
decltype(auto) ret{std::invoke(std::forward<Callable>(op),
    std::forward<Args>(args)...)};
...
return ret;
```

```cpp
struct cleanup {
    ~cleanup() {
        ... // code to perform on return
    }
} dummy;
return std::invoke(std::forward<Callable>(op),
    std::forward<Args>(args)...);
```

basics/invokeret.hpp

```cpp
#include <utility>    // for std::invoke()
#include <functional> // for std::forward()
#include <type_traits> // for std::is_same<> and invoke_result<>

template<typename Callable, typename... Args>
decltype(auto) call(Callable&& op, Args&&... args)
{
    if constexpr(std::is_same_v<std::invoke_result_t<Callable, Args...>, void>) {
        // return type is void:
        std::invoke(std::forward<Callable>(op),
                    std::forward<Args>(args)...);
        ...
        return;
    }
    else {
        // return type is not void:
        decltype(auto) ret{std::invoke(std::forward<Callable>(op),
                                       std::forward<Args>(args)...)};
        ...
        return ret;
    }
}
```

```cpp
if constexpr(std::is_same_v<std::invoke_result_t<Callable, Args...>, void>)
```

```cpp
```cpp
std::remove_const_t<std::remove_reference_t<int const&>>  // int
std::remove_reference_t<std::remove_const_t<int const&>> // int const
```
```

```cpp
std::decay_t<int const&>    // yields int
```

```cpp
make_unsigned_t<int>        //unsigned int
make_unsigned_t<int const&>  // undefined behavior (hopefully error)
```

```cpp
is_copy_assignable_v<int>    // yields true (generally, you can assign an int to an int)
is_assignable_v<int,int>    // yields false (can't call 42 = 42)
```

```cpp
is_assignable_v<int&,int&>  // yields true
```

```cpp
is_swappable_v<int>      // yields true (assuming lvalues)
is_swappable_v<int&,int&>  // yields true (equivalent to the previous check)
is_swappable_with_v<int,int> // yields false (taking value category into account)
```

```cpp
```cpp
template<typename T>
void f (T&& x)
{
    auto p = &x;   // might fail with overloaded operator &
    auto q = std::addressof(x);   // works even with overloaded operator &
    ...
}
```
```

```cpp
```cpp
#include <utility>

template<typename T1, typename T2,
         typename RT = std::decay_t<decltype(true ? std::declval<T1>()
                                                 : std::declval<T2>())>>
RT max (T1 a, T2 b)
{
    return b < a ? a : b;
}
```
```

```cpp
template<typename T>
void f (T&& t)      // t is forwarding reference
{
    g(std::forward<T>(t));  // perfectly forward passed argument t to g()
}
```

```cpp
template<typename T>
void foo(T x)
{
    set(get(x));
}
```

basics/tmplparamref.cpp

```cpp
#include <iostream>

template<typename T>
void tmplParamIsReference(T) {
    std::cout << "T is reference: " << std::is_reference_v<T> << '\n';
}

int main()
{
    std::cout << std::boolalpha;
    int i;
    int& r = i;
    tmplParamIsReference(i);        // false
    tmplParamIsReference(r);        // false
    tmplParamIsReference<int&>(i);  // true
    tmplParamIsReference<int&>(r);  // true
}
```

basics/referror1.cpp

```cpp
template<typename T, T Z = T{}>
class RefMem {
    private:
        T zero;
    public:
        RefMem() : zero{Z} {
        }
};

int null = 0;

int main()
{
    RefMem<int> rm1, rm2;
    rm1 = rm2;            // OK

    RefMem<int&> rm3;     // ERROR: invalid default value for N
    RefMem<int&, 0> rm4;  // ERROR: invalid default value for N

    extern int null;
    RefMem<int&,null> rm5, rm6;
    rm5 = rm6;            // ERROR: operator= is deleted due to reference member
}
```

# basics/referror2.cpp

```cpp
#include <vector>
#include <iostream>

template<typename T, int& SZ>        // Note: size is reference
class Arr {
 private:
    std::vector<T> elems;
 public:
    Arr() : elems(SZ) {              // use current SZ as initial vector size
    }
    void print() const {
        for (int i=0; i<SZ; ++i) {    // loop over SZ elements
            std::cout << elems[i] << ' ';
        }
    }
};

int size = 10;

int main()
{
    Arr<int&,size> y; // compile-time ERROR deep in the code of class std::vector<>

    Arr<int,size> x;  // initializes internal vector with 10 elements
    x.print();        // OK
    size += 100;      // OOPS: modifies SZ in Arr<>
    x.print();        // run-time ERROR: invalid memory access: loops over 120 elements
}
```

```
Arr<int&,size> y; // compile-time ERROR deep in the code of class std::vector<>
```

```cpp
template<typename T>
class optional
{
    static_assert(!std::is_reference<T>::value,
        "Invalid instantiation of optional<T> for references");
    ...
};
```

```cpp
template<typename T>
class Cont {
    private:
        T* elems;
    public:
        ...
};
```

```cpp
struct Node
{
    std::string value;
    Cont<Node> next;        // only possible if Cont accepts incomplete types
};
```

```cpp
template<typename T>
class Cont {
    private:
        T* elems;
    public:
        ...
    typename std::conditional<std::is_move_constructible<T>::value,
            T&&,
            T&
        >::type
        foo();
};
```

```cpp
```cpp
template<typename T>
class Cont {
    private:
        T* elems;
    public:
        template<typename D = T>
        typename std::conditional<std::is_move_constructible<D>::value,
                                  T&&,
                                  T&
                                 >::type
        foo();
};
```
```
