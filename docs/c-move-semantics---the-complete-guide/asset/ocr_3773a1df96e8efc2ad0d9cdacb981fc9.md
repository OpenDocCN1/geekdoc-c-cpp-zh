the function call() calls the function nextString() without any arguments and returns its return value perfectly to initialize s.

When calling

```
auto&& ref = call(returnArg, std::move(s));
```

the function call() calls the function returnArg() with s marked with std::move(). returnArg() returns back the passed argument as an rvalue reference, which then call() perfectly returns to the caller to initialize ref. str still has its value and ref refers to it:

```
s:  Let’s dance
ref: Let’s dance
```

With

```
auto str = std::move(ref);
```

we move the value of both s and ref to str, which means we get the following situation:

```
s:
ref:
str: Let’s dance
```

When calling

```
call(print, std::cout, ref) << '\n';
```

the function call() calls the function print() with std::cout and ref as perfectly forwarded arguments. print() returns the passed stream back as an lvalue reference, which is then returned perfectly to the caller of call().

# 12.2.2 Deferred Perfect Returning

To perfectly return a value that was computed earlier, we have to declare a local object with decltype(auto) and return it with std::move() if and only if it is an rvalue reference. For example:

```
template<typename Func, typename... Args>
decltype(auto) call(Func f, Args&&... args)
{
    decltype(auto) ret{f(std::forward<Args>(args)...)};
    ...
    if constexpr (std::is_rvalue_reference_v<decltype(ret)>) {
        return std::move(ret);  // move xvalue returned by f() to the caller
    }
    else {
        return ret;            // return the plain value or the lvalue reference
    }
}
```

1 Thanks to Matthias Kretz for providing this solution.