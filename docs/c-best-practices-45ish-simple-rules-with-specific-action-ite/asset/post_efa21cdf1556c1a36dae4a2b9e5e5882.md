
# 23. Never Test for this To Be nullptr, It’s UB

*Invalid check for this to be nullptr.*

```cpp
int Class::member() {
    if (this == nullptr) {
        // removed by the compiler, it would be UB
        // if this were ever null
        return 42;
    } else {
        return 0;
    }
}
```

Technically it isn't the check that is Undefined Behavior (UB). But it’s impossible for the check ever to fail. If the this were to be equal to nullptr, you would be in a state of Undefined Behavior.
People used to do this all the time, but it’s always been UB. You cannot access an object outside its lifetime. Compilers today will always remove this check.
The only way it’s theoretically possible for this to be null is when you call a member directly on a null object.

Never Test for this To Be nullptr, It's UB

Bad examples lie ahead, do not repeat them.

Bad call of member on nullptr.

```cpp
Type *obj = nullptr;
obj->do_thing(); // never do this
```

Even in the (technically OK, but never do this) scenario of calling delete this.

Bad example of delete this.

```cpp
struct S {
    std::string data;
}

void delete_yourself() {
    // do things
    delete this; // technically OK

    if (this) {
        // this block will always be executed, nothing changed
        // our view of 'this'
    }

    // never do this
    data.size(); // UB, data's lifetime has ended
}
```

There is no scenario in which a check for if (this) will return false on a modern compiler.

# Exercise: Do you check for this to be nullptr?

A check for nullptr can hide a check for NULL or a check against 0. A check for this to be NULL is likely to only exist in very old code bases. Make sure you have your warnings enabled, then look for these cases.

It's probably interesting in general to search for this == in your codebase and see what weird things are there.

# Resources

- Porting to GCC-6 Optimizations remove null pointer checks for this¹

¹https://www.gnu.org/software/gcc/gcc-6/porting_to.html#this-cannot-be-null

# 24. Never Test for A Reference To Be nullptr, It’s UB

Tests for null references are removed

```cpp
int get_value(int &thing) {
  if (&thing == nullptr) {
    // removed by compiler
    return 42;
  } else {
    return thing;
  }
}
```

It’s UB to make a null reference, don’t try it. Always assume a reference refers to a valid object. Use this fact to your advantage when designing API’s.

# Exercise: Check for checking the address of an object

There are many valid use cases for &thing == to check for a specific address of an object, but there are also ways this check can be wrong.

Search through your code for statements that check an object’s memory address and understand what they are doing and how (or if) they work.

> What other ways might the address of an object be checked besides ====

This exercise gives you some great experience working with various searching / grepping tools and playing with regex.

# Resources

- -Wtautological-undefined-compare¹

https://clang.llvm.org/docs/DiagnosticsReference.html#wtautological-undefined-compare

# 25. Avoid default In switch Statements

This is an issue that is best described with a series of examples. Starting from this one:

```cpp
switch with warnings
enum class Values {
    val1,
    val2
};

std::string_view get_name(Values value) {
    switch (value) {
    case val1: return "val1";
    case val2: return "val2";
    }
}
```

If you have enabled all of your warnings, then you will likely get a “not all code paths return a value” warning here. Which is technically correct. We could call get_name(static_cast<Values>(15)) and not violate any part of C++[dcl.enum/5] except for the Undefined Behavior of not returning a value from a function.

Avoid default In switch Statements

You'll be tempted to fix this code like this:

```cpp
switch with default to avoid warnings

enum class Values {
    val1,
    val2
};

std::string_view get_name(Values value) {
    switch (value) {
        case Values::val1: return "val1";
        case Values::val2: return "val2";
        default: return "unknown";
    }
}
```

But this introduces a new problem

Unhandled case

```cpp
enum class Values {
    val1,
    val2,
    val3 // added a new value
};

std::string_view get_name(Values value) {
    switch (value) {
        case Values::val1: return "val1";
        case Values::val2: return "val2";
        default: return "unknown";
    }
// no compiler diagnostic that `val3` is unhandled
```

Instead, prefer code like this:

# Avoid default In switch Statements

Preferred

```cpp
enum class Values {
    val1,
    val2,
    val3 // added a new value
}

std::string_view get_name(Values value) {
    switch (value) {
        case Values::val1: return "val1";
        case Values::val2: return "val2";
        default: return "unknown";
    }
}
// no compiler diagnostic that `val3` is unhandled
```

# Exercise: Look for default: What do you find in your code?

Some modern tools can detect these for you. Enabling warnings in previous.

# Resources

- CppCon 2018: Victor Ciura “Better Tools in Your Clang Toolbox”¹ (Discusses bugs found by moving to enum class)
- -Wswitch-enum²
- -Wswitch³

¹https://youtu.be/DHOlEd0e
²https://clang.llvm.org/docs/DiagnosticsReference.html#wswitch-enum

# 26. Prefer Scoped enums

C++11 introduced scoped enumerations, intended to solve many common problems with enum.

```cpp
C++98 enums
enum Choices {
    option1 // value in global scope
};

enum OtherChoices {
    option2
};

int main() {
    int val = option1;
    val = option2; // no warning
}
```

- enum Choices;
- enum OtherChoices;

These two can easily get mixed up, and they each introduce identifiers in the global namespace.

- enum Choices;
- enum OtherChoices;

The values in these enumerations are scoped and more typed.

Prefer Scoped enums

```cpp
C++11 scoped enumeration
enum class Choices {
  option1
};

enum class OtherChoices {
  option2
};

int main() {
  int val = option1; // cannot compile, need scope
  int val2 = Choices::option1; // cannot compile, wrong type
  Choices val = Choices::option1; // compiles
  val = OtherChoices::option2; // cannot compile, wrong type
}
```

These enum class versions cannot get mixed up without much effort, and their identifiers are now scoped, not global.

# Exercise: enum struct Or enum class

Decide if you prefer enum struct or enum class and develop a well-reasoned answer as to why.

# Exercise: clang-tidy modernize

Clang-tidy’s modernizer can add class to your enum declarations. Try putting it to use.

> clang-tidy's scoped enumeration modernizer will probably find many bugs in your code!

# Resources

- CppCon 2018: Victor Ciura “Better Tools in Your Clang Toolbox”¹ (Discusses bugs found by moving to enum class)
- cppreference.com Enumeration Declaration^2

¹https://youtu.be/4X_fzkl7kk
2https://en.cppreference.com/w/cpp/enum

# 27. Prefer if constexpr over SFINAE

SFINAE is kind-of-write-only code. if constexpr doesn't have the same flexibility, but use it when you can.

Let's take our divide example last seen in Prefer auto in Many Cases:

```cpp
C++14 divides template.
template<typename Numerator, typename Denominator>
auto divide(Numerator numerator, Denominator denominator)
{
    return numerator / denominator;
}
```
