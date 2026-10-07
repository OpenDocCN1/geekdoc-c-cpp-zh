
## Don't Be Afraid of Templates

Divide ints.

```cpp
int divide(int numerator, int denominator) {
  return numerator / denominator;
}
```

Templates were designed for just this scenario.

Basic template usage.

```cpp
template<typename T>
T divide(T numerator, T denominator) {
  return numerator / denominator;
}
```

Most examples on the internet use T, like I just did. Don't do that. Give your type a meaningful name.

template parameters with actual names.

```cpp
template<typename Arithmetic>
Arithmetic divide(Arithmetic numerator, Arithmetic denominator) {
  return numerator / denominator;
}
```

Exercise: Keep this chapter in mind while moving on to the next chapter and looking at its exercises.

## 19. Don’t Copy and Paste Code

If you find yourself going to select a block of code and copy it: stop!
Take a step back and look at the code again.

- Why are you copying it?
- How similar will the source be to to the destination?
- Does it make sense to make a function?
- Remember, Don’t Be Afraid of Templates

I have found that this simple rule has had the most direct influence on my code quality.
If the result of the paste operation was going in the current function, consider using a lambda.

C++14 style lambdas, with generic (aka auto) parameters, give you a simple and easy to use method of creating reusable code that can be shared with different data types while not having to deal with template syntax.

Exercise: Try CPD.

There are a few different copy-paste-detectors that look for duplicated code in your codebase.
For this exercise, download the PMD CPD tool and run it on your codebase.

> https://pmd.github.io/latest/pmd_userdocs_cpd.html

## Don't Copy and Paste Code

If you use Arch Linux, this tool can be installed with AUR. The package is pmd; the tool is pmd-cpd.

Can you identify critical parts of your code that have been copied and pasted? What happens if you find a bug in one version? Will you be to see all of the locations that also need to be updated?

## Resources

- Copy-Paste Programming²
- The Last Line Effect³
- i will not copy-paste code⁴

> ²https://www.viva64.com/en/t/0068/
³https://www.viva64.com/en/b/0260/
⁴https://twitter.com/bjorn_fahler/status/107243225779987200

## #20. Follow the Rule of 0

No destructor is always better when it's the correct thing to do. Empty destructors can destroy performance:

- They make the type no longer trivial
- Have no functional use
- Can affect inlining of destruction
- Implicitly disable move operations

> If you need a destructor because you are doing resource management or defining a base class with virtual functions, you need to follow the Rule of 5.

std::unique_ptr can help you apply the Rule of 0 if you provide a custom deleter.

Exercise: Find Rule of 0 Violations in Your Code

Look for code like this (I guarantee you will find it):

Empty meaningless destructor.

```cpp
struct S {
  // a bunch of other things
  ~S() {}
};
```

or worse:

Follow the Rule of 0

Forward declared empty meaningless destructor.

```cpp
// file.hpp
struct S {
    ~S();
}
```

```cpp
// file.cpp
S::~S() {
```

Are these destructors necessary? Remove them if they are not.

If these destructors exist in types used in many places, you will likely be able to measure smaller binary sizes and better performance by taking this simple action.

> Some of the pimpl idiom require you to define a destructor. In this case, be sure to follow the Rule of 5.

## Resources

- C++ Reference: The rule of three/five/zero¹
- C++ Weekly Ep 154: “One Simple Trick for Reducing Code Bloat”
- CppCon 2019: Jason Turner “Great C++ is_trivial”³

¹https://en.cppreference.com/w/cpp/language/rule_of_three
²https://youtube.be/D8eCPL2zit4o
³https://youtube.be/ZxWjii99yao

## 21. If You Must Do Manual Resource Management, Follow the Rule of 5

If you provide a destructor because std::unique_ptr doesn’t make sense for your use case, you must must =delete, =default, or implement the other special member functions.

This rule was initially known as the Rule of 3 and is known as the Rule of 5 after C++11.

The special member functions.

```cpp
struct S {
    S(); // default constructor
    // does not affect other special member functions

    // If you define any of the following, you must deal with
    // all the others.
    S(const S&); // copy constructor
    S(S&&); // move constructor
    S&operator=(const S&); // copy assignment operator
    S&operator=(S&&); // move assignment operator
};
```

> =delete is a safe way of dealing with the special member functions you don’t know what to do with them!

You should also follow the Rule of 5 when declaring base classes with virtual functions.

If You Must Do Manual Resource Management, Follow the Rule of 5

Rule of 5 with polymorphic types.

```cpp
struct Base {
    virtual void do_stuff();
```

```cpp
// because of the virtual function we know this class
// is intended for polymorphic use, therefore our
// tools will tell us to define a virtual destructor
virtual ~Base(Base&) = default;
```

```cpp
// and now we need to declare the other special members
// a good safe bet is to delete them, because properly and safely
// copying or assigning an object via a reference or pointer
// to a base class is hard / impossible
```

```cpp
S(S&&) = delete;
S(const&) = delete;
S &operator=(const S&) = delete;
S &operator=(S &&) = delete;
```

```cpp
struct Derived : Base {
// We don't need to define any of the special members
// here, they are all inherited from `Base`.
};
```

> Instead of = delete you can consider making these special members protected.

## Exercise: Implement your unique_ptr<> template

It's hard to get 100% right. Write tests. Understand why the defaulted special member functions don't work.

Bonus points: implement it with C++20's constexpr dynamic allocation support.

## Exercise: Look for Rule of 5 violations in your code

You are likely not providing consistent lifetime semantics in your existing code when you are defining the special member functions. To assess the impact, you can quickly = delete; any missing special member functions and see what breaks.

## Resources

- C++ Reference: The rule of three/five/zero¹

¹https://en.cppreference.com/w/cpp/language/rule_of_three

## 22. Don’t Invoke Undefined Behavior

Ok, there's a lot that's Undefined Behavior (UB), and it's hard to keep track of, so we'll give some examples in the following sections. The critical thing that you need to understand is UB's existence breaks the entire program.

[intro.abstract¹

A conforming implementation executing a well-formed program shall produce the same observable behavior as one of the possible executions of the abstract machine with the same program and the same input.
However, if any such execution contains an undefined operation, this document places no requirement on the implementation executing that program with that input (not even with regard to operations preceding the first undefined operation).

Note the sentence “this document places no requirement on the implementation executing that program with that input (not even with regard to operations preceding the first undefined operation)”

If you have UB, the entire program is suspect.

> The next several items discuss ways to reduce the risk of undefined behavior in your project.

¹http://eel.is/c++draft/intro.compliance#intro.abstract-5

## Exercise: Using UBSan, ASan and Warnings

Understanding all of Undefined Behavior is likely impossible. Fortunately, we have tools that help. Hopefully, you already have your code enabled for UBSan, ASan, and have your warnings enabled. Now is a great time to go back and evaluate what options you have and see if there is anything new you can discover.

## Resources

- C++Now 2018: John Regehr “Closing Keynote: Undefined Behavior and Compiler Optimizations”^2
- CppCon 2018: Barbara Geller & Ansel Sermersheim “Undefined Behavior is Not an Error”^3

> ²2https://youtube.be/AeWxtEOOgH0
3https://youtube.com/XEXpwis_deQ
