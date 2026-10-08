
Similarly to capturing global variables, you'll get the same issues with static objects:

### Capturing Static Variables. Live code @Wandbox

```cpp
#include <iostream>

void bar() {
    static int static_int = 10;
    std::cout << static_int << std::endl;
    auto foo = []() noexcept { return static_int; };
    foo();
    std::cout << static_int << std::endl;
    const auto increase = []() noexcept { ++static_int; };
    increase();
    std::cout << static_int << std::endl;
    const auto moreIncrease = [static_int]()() noexcept { return static_int; };
    moreIncrease();
    std::cout << static_int << std::endl;
}

int main() {
    bar();
}
```

This time we try to capture a static variable and then change its value, but since it has no automatic storage duration, the compiler cannot do it.

The output:

```
10
11
12
13
```

GCC reports a warning when you capture the variable by name [static_int] and Clang shows an error.

## Capturing a Class Member and the Pointer

Things get a bit more complicated when you're in a class member function, and you want to capture a member variable. Since all data members are related to the `this` pointer, it also has to be stored somewhere.

Have a look:

Error when capturing a member variable. Live code @Wandbox

```cpp
#include <iostream>

struct Baz {
void foo() {
    const auto lam = [s]() { std::cout << s; };
    lam();
}

std::string s;

int main () {
    Baz b;
    b.foo();
}
```

The code tries to capture `s` which is a member variable. But the compiler will emit an error message:

In member function 'void Baz::foo()'
error: capture of non-variable 'Baz::s'
error: 'this' was not captured for this lambda function

To solve this issue, you have to capture `this` pointer. Then you'll have access to member variables.

We can update the code to:

```cpp
struct Baz {
    void foo() {
        const auto lam = [this]() { std::cout << s; };
        lam();
    }
    std::string s;
}
```

There are no compiler errors now.

You can use `[=]` or `[&]` to capture `this` (they both have the same effect in C++14).

Please note that we captured `this` by value... to a pointer. That's why you have access to the member variable, not its copy.

In C++11 (and even in C++14) you cannot write:

```cpp
auto lam = ['* this]() { std::cout << s; };
```

The code won't compile in C++11/14; it is, however, allowed in C++17.

If you use your lambdas in the context of a single method, then capturing `this` will be fine. But how about more complicated cases?

Do you know what will happen with the following code?

## Returning a Lambda From a Method

```cpp
#include <functional>
#include <iostream>

struct Baz {
    std::function<void()> foo() {
        return [&] { std::cout << s << std::endl; };
    }
    std::string s;
};

int main() {
    auto f1 = Baz("abc").foo();
    auto f2 = Baz("xyz").foo();
    f1();
    f2();
}
```

The code declares a Baz object and invokes `foo()`. Please note that `foo()` returns a lambda (in `std::function`) that captures a member of the class.

Since we use temporary objects, we cannot be sure what will happen when you call `f1` and `f2`. This is a dangling reference problem and generates Undefined Behaviour.

Similarly to:

```cpp
struct Bar {
    std::string const &() foo() const { return s; }
    std::string s;
};
auto && f1 = Bar("abc").foo(); // a dangling reference
```

Play with code @Wordbox

Again, if you state the capture explicitly (`[s]`):

```cpp
std::function<void()> foo() {
    return [s] { std::cout << s << std::endl; };
}
```

All in all, capturing `this` might get tricky when a lambda can outlive the object itself. This might happen when you use async calls or multithreading.

We'll return to that topic in the C++17 chapter. See this section

## Moveable-only Objects

If you have an object that is movable only (for example `unique_ptr`), then you cannot move it to lambda as a captured variable. Capturing by value does not work; you can only capture by reference.

```cpp
std::unique_ptr<int> p = std::make_unique<int>(10);
auto foo = [p]() {}; // does not compile.
auto foo_ref = [&p]() {}; // compiles, but the ownership
// is not passed
```

In the example, you can see the only way to capture `unique_ptr` by reference. This approach, however, might not be the best as it doesn't transfer the ownership of the pointer.

In the next chapter, about C++14, you'll see this issue is fixed with the capture with initialiser. See this section to follow up on this topic.

## Preserving Const

If you capture a const variable, then the constness is preserved: Preserving const. Live code @Wandbox

```cpp
#include <iostream>
#include <type_traits>

int main() {
    const int x = 10;
    auto foo = [x]() mutable {
        std::cout << std::is_const<decltype(x)>::value << std::endl;
        x = 11;
    };
    foo();
}
```

The above code doesn't compile as the captured variable is constant. The example tried to use mutable, but this doesn't help.

## Capturing a Parameter Pack

To close the capture clause, we should mention that you can also leverage captures with variadic templates. The compiler expands the pack into a list of static members which might be handy if you want to use lambda in templated code. For example, here's a code sample that experiments with captures: Capturing Variadic Pack. Live code @Wandbox

```cpp
#include <iostream>
#include <tuple>

template <class... Args>
void captureTest(Args... args) {
    const auto lambda = [args...]() {
        std::cout << "tuple size: " << std::tuple_size<decltype(args)...>::value << '\n';
        std::cout << "tuple: " << std::make_tuple(args...) << '\n';
    };
    lambda(); // call it
}

int main() {
    captureTest(1, 2, 3);
    captureTest("Hello world", 10);
}
```

After running the code, we'll get the following output:

```
tuple size: 3
tuple: (...)
tuple size: 2
tuple: (...)
```

This somewhat experimental code shows that you can capture variadic parameter pack (by reference is also possible) and then the pack is "stored" into a tuple. We then call helper functions to access its data and properties.

## Return Type

In many cases, you can skip the return type of the lambda and then the compiler will deduce it for you. Initially, return type deduction was restricted to lambdas with bodies containing a single return statement. However, this restriction was quickly lifted as there were no issues with implementing a more convenient version.

To sum up, since C++11, the compiler will be able to deduce the return type as long as all of your return statements are of the same type.

| Condition | Result |
| :--- | :--- |
| lvalue-to-rvalue conversion [conv.val] | |
| array-to-pointer conversion [conv.array] | |
| function-to-pointer conversion [conv.func] | Return Type Deduction. Live code @Wandbox

```cpp
#include <traits>
int main () {
    const auto baz = [](int x) noexcept {
        if (x < 20)
            return x * 1.1;
        else
            return x * 2.1;
    };
    static_assert(std::is_same<double, decltype(baz(10))::value, "has to be the same!");
}
```

In the above lambda, we have two return statements, but they all point to double so the compiler can deduce the type.

> In C++14 return type of lambda will be updated to adapt to the rules of auto deduction for regular functions. See this section.

## Trailing Return Type Syntax

If you want to be explicit about the return type, you can use trailing type specification. For example, when you return a string literal: Returning a string literal from a lambda

```cpp
#include <iostream>
#include <string>

int main() {
    const auto testString = [](int speed) noexcept {
        if (speed > 100) {
            return "you're a super fast";
        }
        return "you're a regular";
    };

    auto str = testString(100);
    str += "driver"; // oops! no += on const char*

    std::cout << str;

    return 0;
}
```

The above code doesn't compile because the compiler dedces const char* as the return type for the lambda. Because there's no += operator available on string literals, so the code breaks.

We can fix the problem by explicitly setting the return type to `std::string`:

```cpp
auto testString = [](int speed) -> std::string {
    if (speed > 100) {
        return "you're a super fast";
    }
    return "you're a regular";
}
```

```cpp
auto str = testString(100);
str += "driver"; // works fine
```

You can play with the code @Coliru

Please notice that we had to remove noexcept now, as the std::string creation might throw.

As a side note, you can also use namespace `std::string_literals;` and then you return "you're a regular"s to indicate the std::string type.
