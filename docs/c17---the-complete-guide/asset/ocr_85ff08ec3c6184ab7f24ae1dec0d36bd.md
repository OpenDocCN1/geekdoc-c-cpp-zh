You might argue that this is what the constructor does already. However, the constructor takes the arguments by reference, which is not the same. In general, even outside templates, arguments passed by value decay, while arguments passed by reference do not decay. Decay means that raw arrays convert to pointers and that top-level qualifiers, such as const, and references are ignored.

Without the deduction guide, for example, when declaring the following:

```
Pair3 p3{"hi", "world"};
```

the type of parameter x is const char(&)[3] and therefore T1 is char[3], and the type of parameter y is const char(&)[6] and therefore T2 is char[6].

Due to the deduction guide, the template parameters decay, which means that passed arrays or string literals decay to the corresponding pointer types. Now, when declaring the following:

```
Pair3 p3{"hi", "world"};
```

the deduction guide is used that takes the parameters by value. Therefore, both types decay to const char*, which is used a deduced template parameters. The declaration has the same effect as if we had declared:

```
Pair3<const char*, const char*> p3{"hi", "world"};
```

Note that the constructor still takes the arguments by reference. The deduction guide is relevant only for the deduction of the template types; it is irrelevant for the actual constructor call after the types T1 and T2 are deduced.

# 9.2.1 Using Deduction Guides to Force Decay

As the previous example demonstrates, in general, a very useful application of these overloading rules is to ensure that a template parameter T decays while it is deduced. Consider a typical class template:

```
template<typename T>
struct C {
  C(const T&) {
  }
  ...
};
```

Here, if we pass a string literal "hello", we pass type const char(&)[6] so that T is deduced as const char[6]:

```
C x{"hello"};    // T deduced as char[6]
```

The reason for this is that template parameter deduction does not decay to the corresponding pointer type when arguments are passed by reference.

With a simple deduction guide

```
template<typename T> C(T) -> C<T>; 
```

we can fix this problem:

```
C x{"hello"};    // T deduced as const char*
```

The deduction guide takes its argument by value and therefore its type decays, which means that "hello" deduces T to be of type const char*.