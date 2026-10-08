
need to be flexible, general, and imply no cost when enabled. This implies simplicity of conception and sophistication in deployment. Here is a scheme that I have used:

Click to view code image

| enum class Error_action { ignore, throwing, terminating, logging }; | Il error-handling alternatives |
| :--- | :--- |
| constexpr Error_action default_Error_action = Error_action::throwing; | Il a default |
| enum class Error_code { range, length_error }; | Il individuals |
| string error_code_name[] = {"range error", "length error"}; | Il names of individual errors |

```cpp
template<Error_action action=default_Error_action, class C>
constexpr void(C cond, Error_code x) // take *if* if the condition "cond" doesn't hold
{
    if (constexpr action == Error_action::logging)
        if (cond) std::cerr << (int)x << " << " << error_code_name[int(x)] << "\n";
    if (constexpr action == Error_action::throwing)
        if (cond) throw x;
    if (constexpr action == Error_action::terminating)
        if (cond) terminate();
    // or no action
}
```

This system might mind-boggling firstly as many of the language features used are not yet presented. However, as required, it is both very flexible and trivial to use. For example:

Click to view code image

```cpp
double& operator[](int i)
{
    expect(i,this) { return 0 && i<size(); Error_code::range_error };
    return element[i];
}
```

This checks if a subscript is in range and throws the default action, throwing an exception, if it is not. The condition expected to hold, `0<=i&&i<size()`, is passed to expect(), i[this](return 0<=i<size()) (§7.3.3). If the constexpr tests are done at compile time (§7.4.3) so that many run-time test is performed for each call of expect(). Action to Error_action::ignore and no action is taken and no code is generated for expect().

By setting Error_action one can select a suitable action for deployment of the program, such as terminating or logging. To support, a table of error_code_names needs to be defined. The logging information could be improved using source_location (§16.5).

In many systems, it is important that an assertion mechanism, such as expect(), offers a single point of control of the meaning of assertion failures. Searching a large code base for if-statements that are really claims of assumptions is typically impractical.

## 4.5.1 assert()

The standard library offers the debug macro, assert(), to assert that a condition must hold at run time. For example:

Click here to view code image

```cpp
void f(const char* p)
{
    assert(p!=nullptr); // p must not be the nullptr
    //...
}
```

If the condition of assert() fails in "debug mode," the program terminates. If not in debug mode, the assert() is not checked. That's pretty crude and inflexible, but often better than nothing.

## 4.5.2 Static Assertions

Exceptions report errors at run. If an error can be found at compile time, it is preferable to do so. That's what most of type system and the facilities for specifying interfaces to user-defined types are. However, we can perform simple checks on properties that are known at compile time and report failures to meet our expectations. The static_assert mechanism can be used for anything that can be expressed in terms of constant expressions (§1.6). For example:

Click here view code image

```cpp
constexpr double C = 299792458; // km/s
void f(double speed)
{
    constexpr double local_max = 160.0/(60*60); // 160.h
    static_assert(speed<C, "can't go fast!");
    static_assert(local_max<C, "can't go fast!"); // error: speed must be a constant
    // OK
    //...
}
```

In general, static_assert(A,S) prints S as a compiler error if A not true. If you don't want a specific message, leave out the S and the compiler will supply a default message:

Click here view code image

```cpp
static_assert(4<=sizeof(int)); // use default message
```

The default message is typically the source location of static_assert plus the asserted predicate. One important use of static_assert is to make assertions about types used as parameters in generic programming (§8.2, §16.4).

## 4.5.3 noexcept

A function that should never throw an exception can be declared noexcept. For example:

Click here view code image

```cpp
void user(int sz) noexcept
{
    Vector v(sz);
    iota(&v[0],&v[sz],1);
    // fill with 1,2,3,4... (see §17.3)
}
```

If all good intent and planning fails, so that user() still throws, std::terminate() is called to immediately terminate the program. Thoughtlessly noexcept is hazardous. If a noexcept calls a function that throws an exception expecting it to be caught and handled, noexcept turns that into a fatal error. Also, noexcept can be complex, error-prone, and expensive (§4.4). Like other powerful language features, noexcept should be applied with understanding and caution.

## 4.6 Advice

- [1] Throw exception to indicate that you cannot perform assigned task; §4.4; [CG: E.2]
- [2] Use exceptions for error handling only; §4.4; [CG: E.3]
- [3] Failing to open a file or reach the end of an iteration are expected events and not exceptional; §4.4.
- [4] Use error codes when immediate handler is called to handle the error; §4.4.
- [5] Throw exception for errors expected to percolate through many function calls; §4.4.
- [6] If in doubt whether to use an exception or an error code, prefer exceptions: §4.4.
- [7] Develop an error-handling strategy in a design; §4.4; [CG: E.12].
- [8] Use purpose-designed user-defined types (not built-in types); §4.2.
- [9] Don't try to catch everything in every function; §4.4; [CG: E.7].
- [10] You may not use the standard-library exception hierarchy; §4.3.
- [11] Prefer RAII to try-blocks; §4.2, §4.3; [CG: E.6].
- [12] Let a constructor establish an invariant, and if it does not throw; §4.3; [CG: E.5].
- [13] Design your error-handling around invariants; §4.3; [CG: E.4].
- [14] What be checked at compile time is usually best checked at compile time; §4.5.2 [CG: P.4][CG: P.5}.
- [15] Use an assertion mechanism to provide a single point of control of the managing of failure; §4.5.
- [16] Concepts (§8.2) are compile-time declarations and therefore often useful in assertions; §4.5.2.
- [17] If your function may throw, declare it noexcept; §4.4; [CG: E.12).
- [18] Don't apply noexcept thoughtfully; §4.5.3.

# 5 Classes

> Those types are not “abstract” they are as real as int and float.
— Doug McIlroy

- Introduction
- Classes
- Concrete Types
  - An Arithmetic Type; A Container; Initializing Containers
- Abstract Types
- Virtual Functions
- Class Hierarchies
  - Benefits from Hierarchies; Hierarchy Navigation; Avoiding Resource Leaks
- Advice

## 5.1 Introduction

This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail:

- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.

The central feature of C++ is the class. A class is a user-defined type provided to represent an entity in the code. Whenever our design for a program has a useful entity, collection of data, etc., we try to represent it as a class in the program so the idea is there in the code, rather than in heads, in a document, or in some comments. Specifically, the support for abstraction and resource management without going into a lot of detail:

- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.
- This chapter and the next three will give you an idea of C++’s support for abstraction and resource management without going into a lot of detail.

- Abstract types
- Virtual functions
- Class hierarchies
- Advice.

The defining characteristic of a concrete type is that its representation is part of its definition.
