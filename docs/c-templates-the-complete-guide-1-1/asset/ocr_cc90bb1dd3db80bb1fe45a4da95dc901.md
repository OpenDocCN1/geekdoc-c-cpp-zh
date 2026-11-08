```
```cpp
double val = 1.2;
strange(val, val);             // OK: with T deduced to double
strange(val, 3.1);             // ERROR: conflicting deductions
combine(val, val);             // ERROR: invalid val
doesn't match declared ...
```
```

The previous principles are only a first approximation, but they cover many cases. Yet there are quite a few common situations that are not adequately explained by these rules. We proceed with a brief discussion of the most important refinements of these rules.

# C.2.1 The Implied Argument for Member Functions

Calls to nonstatic member functions have a hidden parameter that is accessible in the definition of the member function as `this`. For a member function of a class `C`, the hidden parameter is usually of type `C*` (a `const` member function? the hidden parameter is usually of type `C const*`). This is somewhat confusing, since `this` is somewhat of a pointer type. It would have been nicer to make this equivalent to what is now `*this`. However, this was part of an early version of the language reference type from one part of the language, and by the time reference types were added, too much code had already depended on this being a pointer.

The hidden `this` parameter participates in overload resolution just like the implicit parameters. Most of the time this is quite natural, but occasionally it causes unexpected surprises. The following example shows a class that does not work as intended (yet we have seen such code in the real world):

Click here to view code image

```
```cpp
class BString {
public:
    BString(char const*);

    // character access through subscripting:
    char& operator[]
        (std::size_t i)                    // #1
        { return const_cast<char&>(
          static_cast<BString const&>(*this)[i]); }

    char const& operator[]
        (std::size_t i) const              // #2
        { ... }

    // simple conversion to zero-terminated byte string:
    operator char const* () const         // #3
        { ... }
};

int main()
{
    BString str("hello");
    str[5] = 'c'; // possibly an overload resolution ambiguity?
}
```
```

At first, nothing seems ambiguous about the expression `str[5]`. The subscript operator of `str` seems like a perfect match. However, it is not quite perfect because the argument has a type `int`, and the operator expects an unsigned integer type (`std::size_t`), and usually have type- or unsigned? `int` or unsigned `long`, but never type `int`). Still, a simple standard integer conversion makes it easy viable. However, there is another viable candidate: the built-in subscript operator. Indeed, if we apply the implicit conversion operator to `str` (which is the implicit member function parameter), we obtain a pointer type, and now the built-in subscript operator applies. This built-in operator takes an argument of type `std::ptrdiff_t`, which on many platforms is equivalent to `int` and therefore is a perfect match for the argument `5`. So even though the built-in subscript operator is a poor match (by user-defined conversion) for the implicit argument, it is a better match than the operator defined at `#1` for the subscript argument. Hence the potential ambiguity.

It is possible for a set of viable candidates to contain both static and nonstatic members. When comparing a static member with a nonstatic member, the quality of the match of the implicit argument is ignored; only the match between the nonstatic member's parameter types and the argument types is considered.

By default, a nonstatic member function has an implicit `this` parameter that is an lvalue reference type, but C++11 introduced syntax to make it an rvalue reference type. For example:

Click here to view code image

```
```cpp
struct A {
    void f();                       // implicit *this parameter is an
                                    // lvalue reference type
    void f() &&;                    // implicit *this parameter is an
                                    // rvalue reference type
    void f() const;                 // implicit *this parameter is an
                                    // lvalue reference to const
};
```
```

As you can tell from this example, it is possible not only to make the implicit parameter an rvalue reference (with the `&&` suffix) but also to affirm the implicit parameter because the implicit `this` parameter is usually ...