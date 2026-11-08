```
```cpp
template<int N> struct X {
    static int const c = 2;
};

template<> struct X<0> {
    typedef int c;
};

template<typename T> struct Y {
    static int const c = 3;
};

static int const c = 4;

int main()
{
    std::cout << X<10>::c << '\n';
    std::cout << X<0>::c << '\n';
}
```
```

This is a valid C++98 program that outputs 0. It is also a valid C++11 program, but there are three different ways to interpret the parameterized expressions equivalent, and the output is 0 0.

A similar problem existed because of the existence of the digraph `<::` as an alternative for the `[` character (which is not available on some traditional keyboards). Consider the following example:

**Click here to view code image**

```
```cpp
template<typename T>
struct S { };

S<::T> s;              // valid since C++11, but an error before
```
```

Before C++11, that last line of code was equivalent to `S<[:T>` which clearly was invalid. Another “lexical hack” was added to address that problem. When a compiler sees the characters `<::` not immediately followed by `:` or `>`, the leading pair of characters `<:` is not treated as a digraph to `[`. This applies only when the sequence is not followed by one of those characters.

**Click here to view code image**

```
```cpp
#define R(x) #x

int main()
{
    int i = 1, 2, 3, i = 1;    // valid in C++98/03, but an error
                                // in C++11
}
```
```

To understand this, note that the “digraph hack” applies to preprocessing tokens, which are the kinds of tokens acceptable to the preprocessor (they may not be acceptable after preprocessing has completed), and they are decided before macro expansion completes. With that in mind, the C++98/C++03 conditionally transforms `<::` into `[` in the macro invocation, and the definition of `x` transforms to:

```
```cpp
int a[ ] = { 1 };
```
```

which is perfectly fine C++11, however, does not perform the digraph transformation because, before macro expansion, the sequence `<::` is not followed by `:` or `>`. Without the digraph transformation, the concatenation operator is used and the result is a preprocessing token.

```
```cpp
int a[ ] = { 1 };
```
```

# 13.3.2 Dependent Names of Types

The problem with names in templates is that they cannot always be sufficiently classified. In particular, one template cannot look into another template because the contents of that other template can be made invalid by an explicit specialization. The following contrived example illustrates this:

**Click here to view code image**