```
Ptr p1{42};    // deduces Ptr<int*> due to deduction guide
Ptr p2 = 42;   // deduces Ptr<int> due to constructor
int i = 42;
Ptr p3{&i};    // deduces Ptr<int**> due to deduction guide
Ptr p4 = &i;   // deduces Ptr<int*> due to constructor
```

# 9.2.5 Deduction Guides for Aggregates

Deduction guides can be used in generic aggregates to enable class template argument deduction. For example, for:

```
template<typename T>
struct A {
    T val;
};
```

any attempt of class template argument deduction without a deduction guide is an error:

```
A i1{42};        // ERROR
A s1("hi");      // ERROR
A s2{"hi"};      // ERROR
A s3 = "hi";     // ERROR
A s4 = {"hi"};   // ERROR
```

You have to pass the argument for type T explicitly:

```
A<int> i2{42};
A<std::string> s5 = {"hi"};
```

However, after a deduction guide such as:

```
A(const char*) -> A<std::string>;
```

you can initialize the aggregate as follows:

```
A s2{"hi"};      // OK
A s4 = {"hi"};   // OK
```

Note that (as usual for aggregate initialization) you still need curly braces. Otherwise, type T is successfully deduced but the initialization is an error:

```
A s1("hi");      // ERROR: T is string, but no aggregate initialization
A s3 = "hi";      // ERROR: T is string, but no aggregate initialization
```

The deduction guides for std::array are further examples of deduction guides for aggregates.