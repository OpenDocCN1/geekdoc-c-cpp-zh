
the function signature and c++ include some extra header file <functional>
 If you recall from the C++11 chapter, std::function is a heavy object (in
GCC 9 the sizeof shows 32 bytes) and it needs some advanced internal mechanics so that it can handle any callable objects.

Thanks to the improvements in C++14, we can now heavily simplify the
code:

```
Auto return type deduction for lambdas. Live code @Wandbox
#include <iostream>
auto CreateMullLambda(int x) noexcept {
    return [x](int param) noexcept { return x * param; };
}
int main() {
    const auto lam = CreateMullLambda(10);
    std::cout << sizeof(lam);
    return (2);
}
```

This time we can entirely rely on the compile-time type deduction, and no
helper types are required. On GCC the size of lambda sizeof(lam) is just 4
bytes and it's far cheaper than the solution with std::function. Please
notice that we could also mark CreateMullLambda with noexcept as there are no
way it can throw any exception. This was not the case when returning
std::function.

## Captures With an Initialiser

Now some more significant updates!

As you recall, in a lambda expression you can capture variables from the
outside scope. The compiler expands that capture syntax and creates member
variables (non-static members) in the closure type.

Now, in C++14, you can create new member variables and initialise them in
the capture clause. Then you can access these variables inside the lambda.
It's called capture with an initialiser or another name for this feature is
generalised lambda capture.

## For example:

Capture With An Initialiser. Live code @Wandbox

```
#include <iostream>

int main () {
    int x = 30;
    int y = 12;
    const auto foo = [z = x + y]() { std::cout << z << '\n'; };
    x = 0;
    y = 0;
    foo();
}
```

## The output:

42

In the example above, the compiler generates a new member variable and initialises it with x+y. The type of the new variable is deduced in the same way if you put auto in front of this variable. In our case:

```
auto z = x + y;
```

In summary, the lambda from the preceding example resolves into a following (simplified) functor:

```
struct __unnamedLambda {
    void operator()() const {
        std::cout << z << '\n';
    }

    int z;
} someInstance;
```

z will be directly initialised (with x+y) when the lambda expression is defined.

Keep in mind the previous sentence. The new variable is initialised at the place where you define a lambda and not where you invoke it.

That's why if you modify x or y variables after you created the lambda, the variable z won't change. In the example, you can see that immediately after the lambda was defined I changed the values of x and y. The output will be still 42 as z was initialised earlier.

Creating variables through initialiser is also flexible as you can, for example, create a reference to variables from the outside scope.

Reference as Capture With An Initialiser. Live code @Wandbox

```
#include <iostream>
int main() {
    int x = 30;
    const auto foo = [&z = x]() { std::cout << z << '\n'; };
    foo();
    x = 0;
    foo();
}
```

This time the z variable is a reference to x. It's created in the same way as you'd write:

auto & z = x;

If you run the example, you should see that the first line prints 30, but the second line shows 0. This is because we captured a reference so when you modify the referenced variable, the z object will change.

## Limitations

Please note that you can capture with initialiser as a reference, it's not possible to write r-value reference &&. That's why the code below is invalid:

```
[&& z = x] // invalid syntax!
```

Another limitation for the feature is that it doesn't allow parameter packs. Let's have a look at the section 24 of [expr.prim.lambda] :

> A simple-capture followed by an ellipsis is a pack expansion ([temp.variadic)). An init-capture followed by an ellipsis is ill-formed.

In other words, in C++14, you cannot write:

```
template <class... Args>
auto captureTest(Args... args) {
    return lambda = [...capturedArgs] = std::move(args)(){};
    // ...
```

This syntax, however, will be possible with C++20, see in this section.

## Improvements for Existing Issues

All in all, new C++14 feature can solve a few problems, for example with movable only types or allow some extra optimisation.

Let's review now.

## Move

Previously, in C++11, you couldn't capture a unique pointer by value. Only capturing by reference was possible. Now, since C++14, we can move an object into a member of the closure type:

Capturing a movable type code @Wandbox

```
#include <iostream>
#include <memory>

int main() {
    std::unique_ptr<int> p(new int{10});
    const auto bar = [ptr=move(p)] {
        std::cout << "pointer in lambda: " << ptr.get() << '\n';
    };
    std::cout << "pointer in main: " << p.get() << '\n';
bar();
}
```

## The output:

```
pointer in main(): 0
pointer in lambda: 0x1413c20
```

Thanks to the closure initialiser you can move the pointer ownership into lambda. As you can see in the example the unique pointer is set to nullptr just after the closure is created. When you call a lambda, then you'll see a valid memory address.

## One Gotcha with std::function

Having a movable-only captured variable in a lambda makes the closure object not copyable. This might be an issue if you want to store such a lambda in std::function which accepts only copyable callable objects.

We can observe this in detail if we run C++Insights on the previous example

(see this link for a live code) you will see that std::function is a member of the closure type. Having movable-only prevents the default copy constructor.

In short, this won't compile:

```
std::function<void()> fn = [ptr=move(p)]() {};
```

## Optimisation

Another idea is to capture Rather than computing some value every time we invoke lambda, we can compute it once. If you want to you can also look at the proposal P288 which handles movable only types.

Creating a string for lambda. @Wandbox

```
#include <algorithm>
#include <iostream>
#include <string>
#include <vector>

int main() {
  using namespace std::string_literals;
  std::vector<std::string> vs = {"apple", "orange", "foobar", "lemon"};

  const auto prefix = "foo" s;

  auto result = std::find_if(vs.begin(), vs.end(),
      [&prefix](const std::string& s) {
        return s == prefix + "bar" s;
      });

  if (result != vs.end()) {
    std::cout << prefix << "-found! \n";
  }

  result = std::find_if(vs.begin(), vs.end(),
    [savingString=prefix + "bar" s](const std::string& s) {
      return s == savingString;
    });

  if (result != vs.end()) {
    std::cout << prefix << "-found! \n";
  }
}
```

## Capturing a Member Variable

Initialiser is also used to capture a member variable. We can capture a copy of a member variable and don't bother with dangling references.

For example:

```
struct Baz {
  auto foo()const {
    return [s = s](){ std::cout << s << std::endl; }
  }
}

std::string s;

int main () {
  const auto f1 = Baz{"abc"}.foo();
  const auto f2 = Baz{"xyz"}.foo();
  f1();
  f2();
}
```

In foo() we capture a member variable by copying it into the closure type. Additionally, we use auto for the return type of the member function() . As a remark, in C++11, we would have to use std::function.

It might be surprising that we used a "strange" syntax like [s = s] when
