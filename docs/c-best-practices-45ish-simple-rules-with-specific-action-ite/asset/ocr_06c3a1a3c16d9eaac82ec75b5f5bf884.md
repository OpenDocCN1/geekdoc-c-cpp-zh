# Bonus: Understand The Lambda

```
[callable = std::forward<decltype(callable)>(callable),
... xs = std::forward<decltype(param)>(param)
(auto &&...values) {
    auto passed_params =
        std::forward_as_tuple<decltype(values)>(values)...;
    return std::invoke(callable,
        get_param(xs, passed_params)...);
}
};
```

I haven't looked at this code in 2 years, but here is a Compiler Explorer link for you to play with.
https://godbolt.org/z/hhde3P3

# Exercise: Understand the given example and critique it.

What should I have done differently with the above example? Can it be constrained with concepts? Does it need better names? What would you do differently?

³https://godbolt.org/z/hhde3P3