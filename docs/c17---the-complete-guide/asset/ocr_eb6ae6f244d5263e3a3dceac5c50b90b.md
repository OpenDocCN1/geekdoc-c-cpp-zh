# Chapter 14

# Extended Using Declarations

Using declarations were extended to allow a comma-separated list of names, That way using declarations can apply to parameter packs.

For example, you can now program:

```
class Base {
    public:
        void a();
        void b();
        void c();
};
```

```
class Derived : private Base {
    public:
        using Base::a, Base::b, Base::c;
};
```

Before C++17, you needed three different using declarations instead.

# 14.1 Using Variadic Using Declarations

Comma-separated using declarations allow you to generically derive all operations of the same kind from a variadic list of base classes.

A pretty cool application of this technique is to create a set of lambda overloads. By defining the following:

tmpi/overload.hpp

```
// "inherit" all function call operators of passed base types:
template<typename... Ts>
struct overload : Ts...
{
    using Ts::operator()...;
```