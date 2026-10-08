```
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

The code tries to capture s which is a member variable. But the compiler will emit an error message:

In member function 'void Baz::foo()'
error: capture of non-variable 'Baz::s'
error: 'this' was not captured for this lambda function

To solve this issue, you have to capture this pointer. Then you'll have access to member variables.

We can update the code to:

```
struct Baz {
    void foo() {
        const auto lam = [this]() { std::cout << s; };
        lam();
    }
    std::string s;
}
```

There are no compiler errors now.

You can use [=] or [&] to capture this (they both have the same effect in C++14).

Please note that we captured this by value... to a pointer. That's why you have access to the member variable, not its copy.

In C++11 (and even in C++14) you cannot write:

```
auto lam = ['* this]() { std::cout << s; };
```

The code won't compile in C++11/14; it is, however, allowed in C++17.