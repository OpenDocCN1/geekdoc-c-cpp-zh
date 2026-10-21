# 10.2 Using Compile-Time if

In principle, you can use the compile-time if like the runtime if provided the condition is a compile-time expression. You can also mix compile-time and runtime if:

```
if constexpr (std::is_integral_v<std::remove_reference_t<T>>) {
    if (val > 10) {
        if constexpr (std::numeric_limits<char>::is_signed) {
            ...
        }
        else {
            ...
        }
    }
    else {
        ...
    }
}
else {
    ...
}
```

Note that you cannot use if constexpr outside function bodies. Thus, you cannot use it to replace conditional preprocessor directives.

# 10.2.1 Caveats for Compile-Time if

Even when it is possible to use compile-time if, there might be some consequences that are not obvious. These are discussed in the following subsections.²

# Compile-Time if Impacts the Return Type

Compile-time if might impact the return type of a function. For example, the following code always compiles but the return type might differ:

```
auto foo()
{
    if constexpr (sizeof(int) > 4) {
        return 42;
    }
    else {
        return 42u;
    }
}
```

2 Thanks to Graham Haynes, Paul Reilly, and Barry Revzin for bringing all these aspects of compile-time if to my attention.