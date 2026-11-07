**Answer:** True. [Insight: Declaring derived-class functions using the `override` keyword tells the compiler to check whether the base class has a virtual member function with the same signature. If not, the compiler generates an error. This ensures that you override the appropriate base-class function and prevents you from accidentally hiding a base-class function with the same name but a different signature.]

# 10.7.5 virtual Destructors

The C++ Core Guidelines recommend including a **virtual destructor** in *every* class that contains virtual functions.¹³ This helps prevent subtle errors when a derived class has a custom destructor. **In a class that does not have a destructor, the compiler generates one for you, but the generated one is not virtual.** So, in Modern C++, the virtual destructor definition for most classes is written as

```
```cpp
virtual ~SalariedEmployee() = default;
```
```

This enables you to declare the destructor virtual and still have the compiler generate a default destructor for the class—via the notation `= default`.

# Checkpoint

+   1. *(Discussion)* Explain why in Modern C++, the virtual destructor definition for most classes is written as

```
```cpp
virtual ~ClassName() = default;
```
```

**Answer:** This enables you to declare the destructor virtual and still have the compiler generate a default destructor for the class—via the notation `= default`.

# 10.7.6 final Member Functions and Classes

A virtual function that’s declared `final` in its prototype, as in

```
```cpp
returnType someFunction(parameters) final;
```
```

cannot be overridden in any derived class. **In a multilevel class hierarchy, this guarantees that the final member-function definition will be used by all subsequent direct and indirect derived classes.**

You can declare a class `final` to prevent it from being used as a base class, as in

```
```cpp
class MyClass final {
    // class body
};
```
```

or

```
```cpp
class DerivedClass : public BaseClass final {
    // class body
};
```
```

Attempting to override a `final` member function or inherit from a `final` base class results in a compilation error.

¹³. “C.35: A Base Class Destructor Should Be Either public and virtual, or protected and Non-virtual.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rc-dtor-virtual.