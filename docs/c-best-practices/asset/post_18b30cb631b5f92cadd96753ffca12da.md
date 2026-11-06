
*Accidental copy?*

```cpp
std::map<std::string, int> get_map();

using element_type = std::pair<std::string, int>;

for (const element_type &element : get_map())
{
}
```

### Exercise: Enable ranged-loop related warnings

Make sure `-Wrange-loop-construct` is enabled in your code, which is automatically included with `-Wall`.

*Divide ints.*

```cpp
int divide(int numerator, int denominator) {
    return numerator / denominator;
}
```

Templates were designed for just this scenario.

*Basic template usage.*

```cpp
template<typename T>
T divide(T numerator, T denominator) {
    return numerator / denominator;
}
```

Most examples on the internet use T, like I just did. Don't do that. Give your type a meaningful name.

*template parameters with actual names.*

```cpp
template<typename Arithmetic>
Arithmetic divide(Arithmetic numerator, Arithmetic denominator) {
    return numerator / denominator;
}
```

![](img/60cb742bacdfc38724280b0dae4597e3_43_0.png)

**Exercise: Keep this chapter in mind while moving on to the next chapter and looking at its exercises.**

## 19. Don't Copy and Paste Code

If you find yourself going to select a block of code and copy it: stop!
Take a step back and look at the code again.

- Why are you copying it?
- How similar will the source be to the destination?
- Does it make sense to make a function?
- Remember, *Don't Be Afraid of Templates*

I have found that this simple rule has had the most direct influence on my code quality.

If the result of the paste operation was going in the current function, consider using a lambda.

C++14 style lambdas, with generic (aka auto) parameters, give you a simple and easy to use method of creating reusable code that can be shared with different data types while not having to deal with template syntax.

### Exercise: Try CPD.

There are a few different copy-paste-detectors that look for duplicated code in your codebase.

For this exercise, download the PMD CPD tool[^1] and run it on your codebase.

[^1]: https://pmd.github.io/latest/pmd_userdocs_cpd.html

If you use Arch Linux, this tool can be installed with AUR. The package is pmd; the tool is pmd-cpd.

Can you identify critical parts of your code that have been copied and pasted? What happens if you find a bug in one version? Will you be sure to see all of the locations that also need to be updated?

### Resources

- Copy-Paste Programming<sup>2</sup>
- The Last Line Effect<sup>3</sup>
- i will not copy-paste code<sup>4</sup>

<sup>2</sup> https://www.viva64.com/en/t/0068/
<sup>3</sup> https://www.viva64.com/en/b/0260/
<sup>4</sup> https://twitter.com/bjorn_fahller/status/1072432257799987200

## 20. Follow the Rule of 0

No destructor is always better when it's the correct thing to do. Empty destructors can destroy performance:

- They make the type no longer trivial
- Have no functional use
- Can affect inlining of destruction
- Implicitly disable move operations

![](img/60cb742bacdfc38724280b0dae4597e3_46_0.png)

If you need a destructor because you are doing resource management or defining a base class with virtual functions, you need to follow the Rule of 5.

std::unique_ptr can help you apply the Rule of 0 if you provide a custom deleter.

![](img/60cb742bacdfc38724280b0dae4597e3_46_1.png)

### Exercise: Find Rule of 0 Violations in Your Code

Look for code like this (I guarantee you will find it).

Empty meaningless destructor.

```cpp
struct S {
    // a bunch of other things
    ~S() {}
};
```

or worse:

Forward declared empty meaningless destructor.

```cpp
// file.hpp
struct S {
    ~S();
};

// file.cpp
S::~S() {}
```

Are these destructors necessary? Remove them if they are not.

If these destructors exist in types used in many places, you will likely be able to measure smaller binary sizes and better performance by taking this simple action.

> Some uses of the pimpl idiom require you to define a destructor. In this case, be sure to follow the Rule of 5.

### Resources

- C++ Reference: The rule of three/five/zero¹
- C++ Weekly Ep 154: "One Simple Trick for Reducing Code Bloat"²
- CppCon 2019: Jason Turner "Great C++ is_trivial"³

¹ https://en.cppreference.com/w/cpp/language/rule_of_three
² https://youtu.be/D8cCPl2zit4
³ https://youtu.be/ZxWji9syao

## 21. If You Must Do Manual Resource Management, Follow the Rule of 5

If you provide a destructor because `std::unique_ptr` doesn't make sense for your use case, you must `=delete`, `=default`, or implement the other special member functions.

This rule was initially known as the Rule of 3 and is known as the Rule of 5 after C++11.

*The special member functions.*

```cpp
struct S {
    S(); // default constructor
         // does not affect other special member functions

    // If you define any of the following, you must deal with
    // all the others.
    S(const S &);        // copy constructor
    S(S&&);              // move constructor
    S &operator=(const S &); // copy assignment operator
    S &operator=(S &&);  // move assignment operator
};
```

![](img/60cb742bacdfc38724280b0dae4597e3_49_0.png)

`=delete` is a safe way of dealing with the special member functions if you don't know what to do with them!

You should also follow the Rule of 5 when declaring base classes with virtual functions.

Bonus points: implement it with C++20's constexpr dynamic allocation support.

![](img/60cb742bacdfc38724280b0dae4597e3_51_0.png)

### Exercise: Look for Rule of 5 violations in your code

You are likely not providing consistent lifetime semantics in your existing code when you are defining the special member functions. To assess the impact, you can quickly `= delete;` any missing special member functions and see what breaks.

### Resources

- C++ Reference: The rule of three/five/zero¹

¹ https://en.cppreference.com/w/cpp/language/rule_of_three

### Exercise: Using UBSan, ASan and Warnings

Understanding all of Undefined Behavior is likely impossible. Fortunately, we do have tools that help. Hopefully, you already have your code enabled for UBSan, ASan, and have your warnings enabled. Now is a great time to go back and evaluate what options you have and see if there is anything new you can discover.

### Resources

- C++Now 2018: John Regehr “Closing Keynote: Undefined Behavior and Compiler Optimizations”²
- CppCon 2018: Barbara Geller & Ansel Sermersheim “Undefined Behavior Is Not an Error”³

² https://youtu.be/AeEwxEQgH0
³ https://youtu.be/XEXpwis_deQ

## 23. Never Test for this To Be nullptr, It’s UB

*Invalid check for this to be `nullptr`.*

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

Technically it isn’t the check that is Undefined Behavior (UB). But it’s impossible for the check ever to fail. If this were to be equal to `nullptr`, you would be in a state of Undefined Behavior.

People used to do this all the time, but it’s always been UB. You cannot access an object outside its lifetime. Compilers today will always remove this check.

The only way it’s theoretically possible for `this` to be null is when you call a member directly on a null object.

![](img/60cb742bacdfc38724280b0dae4597e3_54_0.png)

Bad examples lie ahead, do not repeat them.

*Bad call of member on nullptr.*

```cpp
Type *obj = nullptr;
obj->do_thing(); // never do this
```

Even in the (technically OK, but never do this) scenario of calling `delete this`.

*Bad example of delete this.*

```cpp
struct S {
  std::string data;

  void delete_yourself() {
    // do things
    delete this; // technically OK

    if (this) {
      // this block will always be executed, nothing changed
      // our view of `this`
    }

    // never do this
    data.size(); // UB, data's lifetime has ended
  }
};
```

There is no scenario in which a check for if (this) will return false on a modern compiler.

![](img/60cb742bacdfc38724280b0dae4597e3_55_0.png)

### Exercise: Do you check for this to be nullptr?

A check for nullptr can hide a check for NULL or a check against 0. A check for this to be NULL is likely to only exist in very old code bases. Make sure you have your warnings enabled, then look for these cases.
