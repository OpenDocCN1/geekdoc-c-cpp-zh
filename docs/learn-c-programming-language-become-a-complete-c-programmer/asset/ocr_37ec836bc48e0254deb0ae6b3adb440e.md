on because of declarations in those classes. I personally don’t (redundantly) use virtual for a function that’s meant to override. For smaller programs (especially with a compiler with decent warnings against common mistakes) getting overriding done correctly isn’t hard. However, for larger hierarchies more specific controls are useful:

+   - **virtual**: The function may be overridden (§20.3.2).
+   - **=0**: The function must be **virtual** and must be overridden (§20.4).
+   - **override**: The function is meant to override a virtual function in a base class (§20.3.4.1).
+   - **final**: The function is not meant to be overridden (§20.3.4.2).

In the absence of any of these controls, a non**static** member function is virtual if and only if it overrides a **virtual** function in a base class (§20.3.2).

A compiler can warn against inconsistent use of explicit override controls. For example, a class declaration that uses **override** for seven out of nine virtual base class functions could be confusing to maintainers.

# 20.3.4.1 override

We can be explicit about our desire to override:

```
struct D : B5 {
void f(int) const override; void g(int) override; virtual int h() override;
};
// error :B0::f() is not virtual
// error :B0::f() takes a double argument // error :no function h() to override
```

Given this definition (and assuming that the intermediate base classes **B1**...**B5** do not provide relevant functions), all three declarations give errors.

In a large or complicated class hierarchy with many virtual functions, it is best to use **virtual** only to introduce a new virtual function and to use **override** on all functions intended as overriders. Using **override** is a bit verbose but clarifies the programmer’s intent.

The **override** specifier comes last in a declaration, after all other parts. For example:

```
void f(int) const noexcept override; // OK (if there is a suitable f() to override)
override void f(int) const noexcept; // syntax error
void f(int) override const noexcept; // syntax error
```

And yes, it’s illogical that **virtual** is a prefix and **override** is a suffix. This is part of the price we pay for compatibility and stability over decades.

An **override** specifier is not part of the type of a function and cannot be repeated in an out-of-class definition. For example:

```
class Derived : public Base { void f() override; void g() override; };
void Derived::f() override {
// ... }
void g() {
// ... }
// OK if Base has a virtual f() // OK if Base has a virtual g()
```