# 4.1 Motivation for Extended Aggregate Initialization

Without this feature, deriving a structure from another type disabled aggregate initialization, which meant that you had to define a constructor:

```
struct Cpp14Data : Data {
    bool done;
    Cpp14Data (const std::string& s, double d, bool b)
        : Data{s,d}, done{b} {
    }
};
```

```
Cpp14Data y{"test1", 6.778, false};
```

Now we have this ability without declaring any constructor. The feature uses the syntax of nested braces, which can be omitted if at least one value is passed:

```
MoreData x{{"test1", 6.778}, false};  // OK since C++17
MoreData y{"test1", 6.778, false};    // OK
```

Note that because this is an aggregate now, other initializations are possible:

```
MoreData u;      // OOPS: value/done are uninitialized
MoreData z{};    // OK: value/done have values 0/false
```

If this is too dangerous, use default member initializers if you can:

```
struct Data {
    std::string name;
    double value{0.0};
};
```

```
struct Cpp14Data : Data {
    bool done{false};
};
```

Alternatively, continue to provide a constructor.

# 4.2 Using Extended Aggregate Initialization

One typical application of aggregate initialization is the ability to initialize members of a C-style structure derived by a class to add additional data members or operations. For example:

```
struct Data {
    const char* name;
    double value;
};
```

```
struct CppData : Data {
    bool critical;
```