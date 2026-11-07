
```cpp
std::string first;  // first name
std::string last;   // last name
public:
  Person(std::string f, std::string l)
    : first{std::move(f)}, last{std::move(l)} {
  }
  ...
};
```

This single constructor takes all possible arguments and ensures that we have only one allocation for each argument.

For example, if we pass two string literals:

`Person p{"Ben", "Cook"};`

we first use them to initialize the parameters f and l:

![](img/7ef3d1ca55bdc192f1cc0929179f3d21_81_0.png)

By using `std::move()`, we move the values of the parameters to the members. First, the member `first` steals the value from `f`:

![](img/7ef3d1ca55bdc192f1cc0929179f3d21_81_1.png)

Then, the member last steals the value from l:

![](img/7ef3d1ca55bdc192f1cc0929179f3d21_82_0.png)

Again, at the end of the constructor, the temporary strings are destroyed. This time it takes less time because the destructors of the strings no longer have to free allocated memory:

![](img/7ef3d1ca55bdc192f1cc0929179f3d21_82_1.png)

This way to initialize the members also works fine if we pass `std::strings`:

- If we pass two existing strings without marking them with `std::move()`, we copy the names to the parameters and move them to the members:

    ```cpp
    std::string name1{"Jane"}, name2{"White"};
    ...
    Person p{name1, name2};        // OK, copy names into parameters and move them to the members
    ```

- If we pass two strings where the value is no longer needed, we do not need any allocation at all:

    ```cpp
    std::string firstname{"Jane"};
    ...
    Person p{std::move(firstname),        // OK, move names via parameters to members
             getLastnameAsString()};
    ```

In this case we move the strings twice: once to initialize the parameters f and l and once to move the values of f and l to the members.

Provided a move is cheap, with this implementation of only one constructor any initialization is possible and cheap.

## 4.3.3 Initialize Members via Rvalue References

There are even more ways to initialize the members of a `Person`, using multiple constructors.

### Using Rvalue References

To support move semantics, we have already learned that we can declare a parameter as a non-const rvalue reference. This allows the parameter to steal the value from a passed temporary object or an object marked with `std::move()`.

Consider we declare the constructor as follows:

```cpp
class Person {
  ...
  Person(std::string&& f, std::string&& l)
    : first{std::move(f)}, last{std::move(l)} {
  }
  ...
};
```

This initialization would also work for our passed string literals:

```cpp
Person p{"Ben", "Cook"};
```

Again, because the constructor needs strings, we would create two temporary strings to which `f` and `l` bind:

![](img/7ef3d1ca55bdc192f1cc0929179f3d21_83_0.png)

And because we have non-const references, we can modify them. In this case, we mark them with `std::move()` so that the initialization of the members can steal the values.

First, the member `first` steals the value from `f`:

### Overloading for Rvalue and Lvalue References

While functions that take rvalue references work fine when we pass temporary objects to them (here, we pass temporary std::strings created from string literals), they also have restrictions: we cannot pass named objects that still need the value afterwards. Therefore, we have only a constructor that takes rvalue references, we cannot pass an existing string:

```cpp
class Person {
  ...
  Person(std::string&& f, std::string&& l)
    : first{std::move(f)}, last{std::move(l)} {
  }
  ...
};

Person p1{"Ben", "Cook"};  // OK

std::string name1{"Jane"}, name2{"White"};
...
Person p2{name1, name2};   // ERROR: can't pass a named object to an rvalue reference
```

For the case of p2 we would need a traditional constructor, which is declared with a const lvalue reference. However, we might also pass a string literal and an existing string. Therefore, in total, we need four constructors for all possible combinations:

```cpp
class Person {
  ...
  Person(const std::string& f, const std::string& l)
    : first{f}, last{l} {
  }
  Person(const std::string& f, std::string&& l)
    : first{f}, last{std::move(l)} {
  }
  Person(std::string&& f, const std::string& l)
    : first{std::move(f)}, last{l} {
  }
  Person(std::string&& f, std::string&& l)
    : first{std::move(f)}, last{std::move(l)} {
  }
  ...
};
```

That way, we can pass both string literals and existing strings in any combination and always have only one allocation per member.

### Overloading Even for String Literals

To improve the performance even more, we might even have specific implementations that take string literals as ordinary pointers. That way, we could avoid even some moves. However, implementing all constructors becomes a bit tedious:

`basics/initiall.hpp`

```cpp
#include <string>

class Person {
 private:
  std::string first;  // first name
  std::string last;   // last name
 public:
  Person(const std::string& f, const std::string& l)
    : first{f}, last{l} {
  }
  Person(const std::string& f, std::string&& l)
    : first{f}, last{std::move(l)} {
  }
  Person(std::string&& f, const std::string& l)
    : first{std::move(f)}, last{l} {
  }
  Person(std::string&& f, std::string&& l)
    : first{std::move(f)}, last{std::move(l)} {
  }
  Person(const char* f, const char* l)
    : first{f}, last{l} {
  }
  Person(const char* f, const std::string& l)
    : first{f}, last{l} {
  }
  Person(const char* f, std::string&& l)
    : first{f}, last{std::move(l)} {
  }
  Person(const std::string& f, const char* l)
    : first{f}, last{l} {
  }
  Person(std::string&& f, const char* l)
    : first{std::move(f)}, last{l} {
  }
  ...
};
```

The benefit of this solution is that we reduce the number of moves. If we pass a string literal, we initialize the members directly with the passed pointer instead of creating a `std::string` and moving its value to the member.

## 4.3.4 Compare the Different Approaches

With the introduction of new ways of initializing members, the obvious question is, which technique should we use when? And also: which technique should we teach?

In general, there should be a good reason not to use the simple approach with `const&`. This reason is usually performance. Therefore, let us measure how long it takes to initialize Persons with three kinds of arguments: passing string literals, passing existing strings, and passing strings marked with `std::move()`.

```cpp
std::string fname = "a first name";
std::string lname = "a last name";

// measure how long this takes:
Person p1{"a firstname", "a lastname"};
Person p2{fname, lname};
Person p3{std::move(fname), std::move(lname)};
```

However, to avoid a short string optimization (SSO), which would mean that the strings do not allocate any memory at all, we should use strings of significant length. So, here is a full function to measure the different approaches:

*basics/initmeasure.hpp*

```cpp
#include <chrono>

// measure num initializations of whatever is currently defined as Person:
std::chrono::nanoseconds measure(int num)
{
    std::chrono::nanoseconds totalDur{0};
    for (int i = 0; i < num; ++i) {
        std::string fname = "a firstname a bit too long for SSO";
        std::string lname = "a lastname a bit too long for SSO";

        // measure how long it takes to create 3 Persons in different ways:
        auto t0 = std::chrono::steady_clock::now();
        Person p1{"a firstname too long for SSO", "a lastname too long for SSO"};
        Person p2{fname, lname};
        Person p3{std::move(fname), std::move(lname)};
        auto t1 = std::chrono::steady_clock::now();
        totalDur += t1 - t0;
    }
    return totalDur;
}
```
