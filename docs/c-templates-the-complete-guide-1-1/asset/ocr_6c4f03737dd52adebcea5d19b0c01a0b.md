# 17.2 GENERALIZED NONTYPE TEMPLATE PARAMETERS

Among the restrictions on nontype template arguments, perhaps the most surprising to beginning and advanced template writers alike is the inability to provide a string literal as a template argument.

The following example seems intuitive enough:

Click here to view code image

```
```cpp
template<char const* msg>
class Diagnoser {
public:
    void print();
};

int main()
{
    Diagnoser<"Hello"> d;
}
```
```

However, there are some potential problems. In standard C++, two instances of `Diagnoser` are the same type if and only if they have the same arguments. In this case the argument is a pointer value—in other words, an address. However, two identical string literals appearing in different source locations are not required to have the same address. We could thus find ourselves in the awkward situation that `Diagnoser<"X">` and `Diagnoser<"X">` are in fact two different and incompatible types! (Notice that the type of `"X"` is `char const[2]`, but it decays to `char const*` when passed as a template argument.)

Because of these (and related) considerations, the C++ standard prohibits string literals as arguments to templates. However, some implementations might not offer this facility as an extension. They enable this by using the natural string literal identity in their implementations of template arguments. Although this is clearly feasible, some C++ language committees feel that a nontype template parameter that can be substituted by a string literal value should be declared differently from one that can be substituted by an address. One possibility would be to capture string literals as a parameter pack of characters. For example:

Click here to view code image

```
```cpp
template<char...>
class Diagnoser {
public:
    void print();
};

int main()
{
    Diagnoser<'H', 'e', 'l', 'l', 'o'> d;
}
```
```

We should also note an additional technical wrinkle in this issue. Consider the following template declarations, and let's assume that the language has been extended to accept string literals as template arguments in this case:

Click here to view code image

```
```cpp
template<char const* str>
class Bracket {
public:
    static char const* address();
    static char const* value();
};

template<char const* str>
char const* Bracket<str>::address()
{
    return str;
}

template<char const* str>
char const* Bracket<str>::value()
{
    return str;
}
```
```

In the previous code, the two member functions are identical except for their names—a situation that is not that uncommon. Imagine that an implementation would instantiate `Bracket<"str">` using a process much like macro expansion: In this case, if the two member functions are instantiated in different translation units, they may return different values. Interestingly, a trait of some C++ compilers that currently provide this extension reveals that they do suffer from this surprising behavior.

A related issue is the ability to provide floating-point literals (or single constant floating-point expressions) as template arguments. For example:

Click here to view code image

```
```cpp
template<double Ratio>
class Converter {
public:
    static double convert(double val) {
        return val * Ratio;
    }
};

using InchToMeter = Converter<0.0254>;
```
```