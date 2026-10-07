# 25. Avoid default In switch Statements

This is an issue that is best described with a series of examples. Starting from this one:

```
switch with warnings
enum class Values {
    val1,
    val2
};

std::string_view get_name(Values value) {
    switch (value) {
    case val1: return "val1";
    case val2: return "val2";
    }
}
```

If you have enabled all of your warnings, then you will likely get a “not all code paths return a value” warning here.Which is technically correct. We could call get_name(static_cast<Values>(15)) and not violate any part of C++[dcl.enum/5] except for the Undefined Behavior of not returning a value from a function.