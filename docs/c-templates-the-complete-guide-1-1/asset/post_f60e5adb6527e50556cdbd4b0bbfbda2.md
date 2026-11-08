
The previous principles are only a first approximation, but they cover many cases. Yet there are quite a few common situations that are not adequately explained by these rules. We proceed with a brief discussion of the most important refinements of these rules.

### C.2.1 The Implied Argument for Member Functions

Calls to nonstatic member functions have a hidden parameter that is accessible in the definition of the member function as `this`. For a member function of a class `C`, the hidden parameter is usually of type `C*` (for a `const` member function, the hidden parameter is usually of type `C const*`). This is somewhat confusing, since `this` is a pointer type. It would have been nicer to make `this` a reference type. However, `this` was part of an early version of the language, and by the time reference types were added, too much code had already depended on `this` being a pointer.

The hidden `this` parameter participates in overload resolution just like other parameters. Most of the time this is quite natural, but occasionally it causes unexpected surprises. The following example shows a class that does not work as intended (yet we have seen such code in the real world):

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

At first, nothing seems ambiguous about the expression `str[5]`. The subscript operator of `str` seems like a perfect match. However, it is not quite perfect because the argument has a type `int`, and the operator expects an unsigned integer type (`std::size_t`, which on many platforms is `unsigned int` or `unsigned long`, but never `int`). Still, a simple standard integer conversion makes it easily viable. However, there is another viable candidate: the built-in subscript operator. Indeed, if we apply the implicit conversion operator to `str` (which is the implicit object argument), we obtain a pointer type, and now the built-in subscript operator applies. This built-in operator takes an argument of type `std::ptrdiff_t`, which on many platforms is equivalent to `int` and therefore is a perfect match for the argument `5`. So even though the built-in subscript operator is a poor match (by user-defined conversion) for the implicit argument, it is a better match than the operator defined at `#1` for the subscript argument. Hence the potential ambiguity.

It is possible for a set of viable candidates to contain both static and nonstatic members. When comparing a static member with a nonstatic member, the quality of the match of the implicit argument is ignored; only the match between the nonstatic member's parameter types and the argument types is considered.

By default, a nonstatic member function has an implicit `this` parameter that is an lvalue reference type, but C++11 introduced syntax to make it an rvalue reference type. For example:

```cpp
struct A {
    void f();                       // implicit *this parameter is an
                                    // lvalue reference type
    void f() &&;                    // implicit *this parameter is an
                                    // rvalue reference type
    void f() const &;               // implicit *this parameter is an
                                    // lvalue reference to const
};
```

As you can tell from this example, it is possible not only to make the implicit parameter an rvalue reference (with the `&&` suffix) but also to const-qualify the implicit parameter. The implicit `this` parameter is usually an lvalue reference; that reference is the traditional implicit “this” parameter, but that (somewhat dangerous) special case no longer applies if the rvalue reference treatment was requested explicitly. So, with the definition of `f` specified above:

```cpp
int main()
{
    A a;
    a.f();              // OK
    A{}.f();            // OK: old rule allows rvalue to
                        // match lvalue reference?
    const A{}.f();      // ERROR: rvalue cannot match an
                        // lvalue reference type of this
}
```

### C.2.2 Refine the Perfect Match

For an argument type X, there are four common parameter types that constitute a perfect match: X, X&, const X& (const X is also an exact match, but it is rarely used). However, it is not common to overload a function on two kinds of reference. Prior to C++11, this meant cases like these:

```cpp
void report(int);        // #1
void report(const int&); // #2

int main()
{
    for (int k = 0; k < 4; ++k)
        report(k);         // calls #1

    report(42);            // calls #2
}
```

Here, the version without the extra const is preferred for lvalues, whereas only the version with const can match rvalues.

With the addition of rvalue references in C++11, another common case of two perfect matches needing to be distinguished is illustrated by the following example:

```cpp
struct Value {
};

void pass(Value&);        // #1
void pass(Value&&);       // #2

void g(Value x)
{
    pass(x);              // calls #1, because x is an
                          // lvalue
    pass(Value{});        // calls #2, because Value{} is an
                          // rvalue
    pass(std::move(x));   // calls #2, because x is an
                          // rvalue
}
```

This time, the version taking an rvalue reference is considered a better match for rvalues, but it cannot match lvalues.

Note that this also applies to the implicit argument of a member function call:

```cpp
class Wonder {
public:
    void tick();          // #1
    void tick() const;    // #2
    void tick() const&&;  // #3
};

void run(Wonder& device)
{
    device.tick();                 // calls #1
    const Wonder& cdevice = device;
    cdevice.tick();                // calls #2, because there
                                   // is no non-const version
    std::move(cdevice).tick();     // calls #3
}
```

Finally, the following modification of our earlier example illustrates that perfect matches can create an ambiguity if you overload with and without reference:

```cpp
void report(int);          // #1
void report(int const&);   // #2
void report(int const&&);  // #3

int main()
{
    for (int k = 0; k < 4; ++k)
        report(k);          // ambiguous #1 and #2 match

    report(42);             // ambiguous #1 and #3 match
}
```

## C.3 Overloading Details

The previous section gave most of the overloading situations encountered in everyday C++ programming. There are, unfortunately, many more rules and exceptions to these rules—more than is reasonable to present in a book that is really about C++ templates. Nonetheless, we discuss some of them here in part because they apply somewhat more often than other rules and in part to provide a reason for how deep the details go.

### C.3.1 Prefer Nontemplates or More Specialized Templates

When all other aspects of overload resolution are equal, a nontemplate function is preferred over an instance of a template (it doesn't matter whether that instance is generated from the generic template definition or whether it is provided as an explicit specialization). For example:

```cpp
template<typename T> int f(T);    // #1
void f(int);                    // #2

int main()
{
    return f(1);    // ERROR: rejects #2, which doesn't
                    // return a value
}
```

This example also clearly illustrates that overload resolution normally does not involve the return type of the selected function.

However, when other aspects of overload resolution slightly differ (such as having different const and reference qualifiers), then the general rules of overload resolution apply. This effect can easily accidentally cause surprising behavior when member functions are defined that accept the same arguments as copy or move constructors. See Section 16.2 on page 333 for details.

If the choice is between two templates, then the most specialized of the templates is preferred (provided one is actually more specialized than the other). See Section 6.2.2 on page 330 for a thorough explanation of this concept. One special case of this distinction occurs when two templates only differ in the order of their template parameter packs: the template with the more specialized parameter pack is considered more specialized and is therefore preferred if it matches the call. Section 4.4 on page 53 discusses an example of this situation.

### C.3.2 Conversion Sequences

An implicit conversion can, in general, be a sequence of elementary conversions. Consider the following code example:

```cpp
class Base {
public:
    operator short() const;
};

class Derived : public Base
{};

void count(int);

void process(Derived const& object)
{
    count(object);    // matches with user-defined conver-
                      // sion
}
```

The call `count(object)` works because `object` can implicitly be converted to `int`. However, this conversion requires several steps:

- 1. A conversion of `object` from `Derived const` to `Base const` (this is a glvalue conversion; it preserves the identity of the object).
- 2. A user-defined conversion of the resulting `Base const` object to type `short`.
- 3. A promotion of `short` to `int`.

This is the most typical kind of conversion sequence: a standard conversion (a derived-to-base conversion, in this case), followed by a user-defined conversion, followed by another standard conversion. Although there can be at most one user-defined conversion in a conversion sequence, there can be several standard conversions in a conversion sequence.

An important principle of overload resolution is that a conversion sequence that is a subsequence of another conversion sequence is preferable over the latter sequence. If there were an additional candidate function

```cpp
void count(short);
```

in the example, it would be preferred for the call `count(object)` because it doesn't require the third step (promotion) in the conversion sequence.

### C.3.3 Pointer Conversions

Pointers and pointers to members undergo special standard conversions, including:

- Conversions to type `bool`.
- Conversions from an arbitrary pointer type to `void*`.
- Derived-to-base conversions for pointers.
- Base-to-derived conversions for pointers to members.

Although all of these can cause a match with standard conversions only, they are not ranked equally.
