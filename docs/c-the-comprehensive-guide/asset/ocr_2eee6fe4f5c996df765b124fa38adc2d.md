You are not alone in this. Therefore, there is a way to define a functor directly on the spot where it is needed, as the third parameter in `sort()`. You write the function body of `operator()` directly at the appropriate place:

```
std::ranges::sort(dwarves,
    [](const Dwarf& a, const Dwarf& b) { return a.year_<b.year_; }
);
```

As you can see, you also need to inform the compiler with `(const Dwarf& a, const Dwarf& b)` about what the parameters of `operator()` actually are. The construct is introduced with `[]`. In the past, before C++20 ranges, you would write `std::sort(begin(dwarves), end(dwarves), ...)`.

You have just created an *anonymous function*. Except for the name, you have all the elements of a function definition.

What is still missing—and you have surely noticed this—is the return type. The compiler can infer it in most cases. If you want (or need) to specify it explicitly for an anonymous function, then use the trailing `->` notation:

```
std::ranges::sort(dwarves,
    [](const Dwarf& a, const Dwarf& b) -> bool { return a.year_<b.year_; }
);
```

You can translate any lambda expression directly into a functor class with a name. The anonymous function

```
std::ranges::sort(dwarves,
    [](const Dwarf& a, const Dwarf& b) -> bool { return a.year_<b.year_; }
);
```

becomes the following:

```
struct F {
    bool operator()(const Dwarf& a, const Dwarf& b) const
    {
        return a.year_<b.year_;
    }
};
std::sort(begin(dwarves), end(dwarves), F{});
```

Perhaps this transformation will help you understand.

# Lambdas with External Access

Within the statement block of the anonymous function, you cannot access surrounding variables. Why would you want to do something like that? A typical use case is, for example, a variable that, unlike the arguments of the `const Dwarf& a` and `const Dwarf& b` lambda, does not change with each call. You might only change the general behavior of the comparison.