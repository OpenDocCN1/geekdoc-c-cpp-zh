
as auto template parameters.

For a lambda:

```
[(auto x) { x; }
```

The compiler generates a call operator that corresponds to the following template method:

```
template < typename T>
void operator()(T x) { x; }
```

But there was no way to change this template parameter and use “real” template arguments. With C++20 it is possible now.

For example, how can we restrict our lambda to work only with vectors of some type?

We can write a generic lambda:

```cpp
auto foo = [](auto & vec) {
  std::cout << std::size(vec) << '\n';
  std::cout << vec.capacity() << '\n';
};
```

But if you call it with an int parameter (like foo(10) ) then you might get some hard-to-read error:

```
prog.cc: In instantiation of
'main()::<lambda(const auto:1)> [with auto:1 = int]'
prog.cc:16:11: required from here
prog.cc:11:30: error: no matching function for call to 'size(const int&)'
11 | std::cout<<std::size(vec) << '\n';
```

In C++20 we can write:

```cpp
auto foo = []<typename T>(std::vector<T> const & vec) {
  std::cout << std::size(vec) << '\n';
  std::cout << vec.capacity() << '\n';
};
```

The above lambda resolves to a templated call operator:

```
< typename T>
void operator() (std::vector<T> const & s) { ... }
```

The template parameter comes after the capture clause [ ].

If you call it with int (foo(10); ) then you get a nicer message:
note: mismatched types 'const std::vector<T>' and 'int'

Play with code @Wandbox

In the above example, the compiler can warn you about the mismatch in the interface of the lambda.

Another important aspect is that in the generic lambda example, you only have a variable and not its template type. If you want to access the type, you have to use decltype(x) (for a lambda with (auto x) argument). This makes code more wordy and complicated.

For example (using code from P0428):

```cpp
Deducing from generic argument
auto f = []<auto const &x> {
  using T = std::decay_t<decltype(x)>;
  T copy = x;
  T::static_function();
  using iterator = typename T::iterator;
}
```

Can be now written as:

```cpp
auto f = []<typename T>(T const & x) {
  T copy = x;
  T::static_function();
  using iterator = typename T::iterator;
}
```

As you can see above, in the first example we need to write:

```
using T = std::decay_t<decltype(x)>
```

To get the type of the input argument, in the C++20 version, there's no need for this as we can access the template parameter.

And another important use case is perfect forwarding in a generic variadic lambda:

```cpp
// C++17
auto ForwardToTestFunc = [](auto... args) {
    // what's the type of args ?
    return TestFunc(std::forward<decltype(args)>(args)...);
};
```

Each time you want to access the type of the template argument, you need to use decltype() , but with template lambdas there's no need for that:

```cpp
// C++20:
auto ForwardToTestFunc = []<typename... T>(T&& ...args) {
    return TestFunc(std::forward<T>(args...)); // we have all the types!
};
```

As you can see, template lambdas provide cleaner syntax and better access to types of arguments.

But there's more! You can also use concepts with lambdas! See in the next section.

# Concepts and Lambdas

Concepts are a revolutionary approach for writing templates! They allow you to put constraints on template parameters which improve the readability of code, might speed up compilation time and give better error messages.

One simple example:

```cpp
// define a concept:
template < class T>
concept SignedIntegral = std::is_integral_v<T> && std::is_signed_v<T>;

// use:
template < SignedIntegral T>
void signedIntOnly(T val) { }
```

In the code above we create a concept that describes types that are signed and integral. Please notice that we can use existing traits. Later, use it to define a template function that supports only types that match the concept. Here we don't use typename but we can refer to the name. Ok, but is that related to lambda expressions?

# Simplifications and Terse Syntax

The key part here is the terse syntax and constrained auto. Thanks to the terse concept syntax you can also write templates without `template<typename>` part.

```cpp
With unsigned auto :
void myTemplateFunc (auto param) { }

Or with signed auto :
void signedIntOnly (SignedIntegral auto) { }

With floating_point auto (fp) { }
```

Such syntax is similar to what you could use in generic lambdas from C++14. In other words, lambdas can leverage this style and put extra restrictions on the generic argument:

```cpp
auto GenLambda = [](SignedIntegral auto param) { return param + 1; };
```

As you can see in the above example, I restricted the auto with SignedIntegral concept. The whole expression is even more readable than the lambda that discussed in the previous section. Here's a bit more complicated example, where we can even define a concept of some class interface:

```cpp
template < typename T>
concept Renderable = requires(T v) {
  (v.render()) -> std::same_as<void>;
  (v.getCount()) -> std::convertible_to<size_t>;
};
```

In the above example we define a concept that matches all types with `render()` and `getCount()` member functions. We can use it to write a generic lambda:

```cpp
// Implementation of Renderable interface
#include <concepts>
#include <iostream>

template < typename T>
concept Renderable = requires(T v) {
    (v.render()) -> std::same_as<void>;
    (v.getCount()) -> std::convertible_to<size_t>;
};

struct Circle {
    void render() { std::cout << "drawing circle" };
    size_t getCount() const { return 10; };
};

struct Square {
    void render() { std::cout << "drawing square" };
    size_t getCount() const { return 4; };
};

int main () {
    const auto RenderCaller = [](Renderable auto& obj) {
        obj.render();
    };

    Circle c;
    RenderCaller(c);
    Square s;
    RenderCaller(s);
}
```

In the above example RenderCaller is a generic lambda which can support types that satisfies the Renderable concept.

# Changes to Stateless Lambdas

You might recall from the chapter about C++11 lambdas, even stateless, are not constructible. However, this limitation is lifted in C++20.

That's why, if your lambda doesn't capture anything, then you can write the following code:

```cpp
// A stateless lambda
#include <set>
#include <string>
#include <iostream>

struct Product {
    std::string _name;
    int _id { };
    double _price { 0.0 };
}

int main() {
    const auto nameCmp = [](const auto & a, const auto & b) {
        return a.__name < b.__name;
    };
    const std::set<Product, decltype(nameCmp)> prodSet {
        {"Cup", 10, 100.0}, {"Book", 2, 200.5},
        {"TV set", 1, 2000}, {"Pencil", 4, 10.5}
    };

    for (const auto & elem : prodSet) {
        std::cout << elem.__name << '\n';
    }
}
```

In the preceding example, I declared a class that stores a list of Products. I need a way to compare products, so I passed a stateless lambda that compares their string names.

For example, if you compiled that code with a C++17 flag, then you'd get an error about using a deleted constructor:

```
stl_set.h:In constructor
'std::set<_Key, _Compare, _Alloc>...
[with _Key = Product;
  _Compare = main()::lambda(const auto&1, const auto&2)>;
stl_set.h:244:29: error: use of deleted function
'main()::lambda(const auto&1, const auto&2)>:::<lambda()'
```

But in C++20 you can store stateless lambdas and even copy them:

```cpp
template < typename F>
struct Product {
    int _id {};
    double _price { 0.0 };
    F _predicate;
};

int main() {
    const auto idCmp = [](const auto &a) noexcept {
        return a._id != 0;
    };
    Product p { 10, 2000.0, idCmp };
    [[maybe_unused]] p2 = p;
}
```

# Even more with unvaluated contexts

There are also changes related to advanced use cases like unvaluated contexts. All together with default constructible lambdas you can now write:
