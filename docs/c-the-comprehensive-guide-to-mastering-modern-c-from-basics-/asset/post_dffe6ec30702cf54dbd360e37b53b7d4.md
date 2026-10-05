
```cpp
std::cout << b << '\n';
// Output: 42
}
```

**Listing 13.19** The compiler determines whether the call can be evaluated at compile time in the given context.

Although a is not evaluated in a constexpr context, if consteval detects that the caller is not constant and inserts the else branch at this point during compilation. For b, however, the if branch is used because b is constexpr and can be evaluated at compile time.

This is just another way of writing the following:

```cpp
constexpr int get_value() {
  if(std::is_constant_evaluated()) {
    return 42;
  } else {
    return 668;
  }
}
```

Because this was often confused with if constexpr, the new syntax was introduced.

must not tell anyone. And don't use it, okay? You can make a field mutable in a class, even if you are currently in a const method.

By doing this, you bypass the assurance that the compiler provides you. But sometimes you have to make an exception. For example, if you want to count the number of calls to a method for analysis purposes, which is actually const.

```cpp
// https://godbolt.org/z/zSPorKnEbd
#include <iostream>
class Data {
    int value_;
    mutable size_t getCount_;
public:
    explicit Data(int v) : value_(v) {}
    ~Data() {
        std::cout << "get was used " << getCount_ << " times\n";
    }
    int get() const {
        ++getCount_;
        return value_;
    }
};
int main() {
    Data d(42);
    for(int i=0; i<10; ++i) { d.get(); }
    // Output: get was used 10 times
```

**Listing 13.20** “mutable” makes a data field in const methods mutable.

If you were to omit mutable, the ++getCount_ expression in get() would be an error. In methods marked with const, it is not possible to modify instance data fields. With mutable, you make an exception for a single field.

And you should treat mutable as an exception: it only for analysis. If you need it for another reason, reconsider your design.

You can also append a mutable to a lambda. I describe this more detail in Chapter 23, Section 23.3.6 under the “Mutable Lambdas” section.

| 13.10.11 | Const-Correctness | A related and very helpful aspect in the Long run is to get used to the correct use of const. Coming from C (or Java), this probably means using more of it. Once in the C++ world, the compiler can already uncover many logical errors in the code with const in the right places—where something was changed that was not meant to be changed. |

The second aspect is documentation. A const tells subsequent programmers (all too often yourself) what this value is intended for. Is the variable used for computation, or just for temporary storage? Is it an input parameter or an output parameter?

# Iterators for Constants

In addition, there are other places where the immutability of a value can be indicated. I will go into iterators in more detail in Chapter 20, but as they are somewhat constant, I should explain them here.

A Container::const_iterator is a reference into a standard library container that does not modify the elements within. It should be considered similar to int const*: the value cannot be changed, but the reference can. Thus, it is different from Container::iterator, which is comparable to an int const. The iterator itself remains fixed.

```cpp
// https://cppbolt.org/z/GE5v6Ea8x
#include <map>
#include <string>
using std::map; using std::string;
struct MyClass {
    bool isFound(const map<int,string> &dict, // immutable input
    parameter);
```

# **Listing 13.21** "const" with containers.

The find method returns an iterator. However, it can be implicitly converted to a const_iterator. The other way around would not work implicitly.

> If you equip your program with 13.10.12 Summary many consts as possible—or—from the beginning, then the compiler can detect many typos, logical errors, and sometimes even design errors during development.

The interface of classes and functions is described rudarily with const but without explicit documentation. In the program code, your future audience will thank you because const helps them understand what was meant to be changed and what was not.

Making a project const-correct from the beginning takes far less effort than having to do it later for debugging purposes.

The correct use of const is a powerful, not to be underestimated tool. It is better to start with “many” consts and consider whether you can omit them at a certain point rather than consider whether you should add more.

Using const correctly is part of type-safe programming. C++ has a powerful type system for error prevention. Use C++'s capabilities to operate on types at compile time and to compute with them.

## 13.11 Volatile with “volatile”

The const and volatile keywords are often mentioned together. There are two reasons for this: first, they form the common group of cv-qualifiers in the standard; and second, volatile is somewhat the opposite of const. With volatile, you mark things that can change. The compiler should neither apply optimizations nor copy these variables into a register for calculations, for example. All calculations must be done directly in the memory.

## C++20: Fewer “volatile”

Historically, volatile can appear anywhere const. This is nonsensical and confuses both programmers and compiler alike. Just because a parameter can be const, this was also allowed for volatile, which is pointless:

```cpp
int func(volatile int x); // volatile is pointless
```

Since C++20, volatile has been significantly pruned. By and large, volatile variables still serve the purpose of interacting with the external world. For example, for instance, if you want to read a temperature sensor on your Raspberry Pi via the general-purpose input/output (GPIO) interface, one way to do this is to access the GPIO pin through a volatile variable.

**Listing 13.22** x and y fields of Pos have been

The x and y fields of Pos have been qualified with volatile. This tells the compiler that the values could change at any time. There are (especially since C++20) rules about what you should not do with a volatile variable:

- Do not use it as a synchronization mechanism between threads. There are other mechanisms that are better and safer for this purpose.
- Do not use compound assignments like x += 1 or v |= 0x03 on a volatile variable. It may—but does not have—result in two accesses to the variable, which would be inconsistent. However, you may write x = x+1 or v = v | 0x03 as it is clear that there is one read and write operation. Also, +++ is allowed.

# 14 GOOD CODE, 3RD DAN: TESTING

Professionalism must be pursued in software development in all phases: in planning, communication, programming (of course), testing, quality assurance, documentation, and, last but not least, maintenance.

The aspect of programming in C++ is the main focus of this book. In this chapter, I would like to introduce to another part of this chain, which also has a lot to do with C++: testing.

## Requirements for Tests

There are several requirements for tests themselves. These are some important criteria roughly in order of their importance:

1. Tests must be meaningful.
2. Good tests provide reproducible results.
3. They should be as automated as possible.
4. They should be able to be conducted regularly.
