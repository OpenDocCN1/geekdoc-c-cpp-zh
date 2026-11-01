the compiler will treat Ramanujan as an integer, populating the memory consumed by the definition with the correct bit pattern. Similarly, if you write

```
auto Ramanujan = 1729u;
```

or

```
auto Ramanujan = 1729.f;
```

the compiler will infer the type from the assignment (unsigned int and float, respectively) and correctly populate the memory.

All this machinery exists so that you do not need to worry about representation. The less time you spend programming with types and the more time you spend programming with interfaces, the safer your code will be.

# Union

There are several ways of subverting type safety, most of which are legacies from C. Consider the union keyword.

```
union converter {
    float f;
    std::uint32_t ui;
};
```

This declares a type whose contents may be interpreted as either a float or an unsigned integer. As demonstrated above, this is a road to regret and a pathway to perdition. The programmer is required to know, at all times, which type is being represented. They are entirely entitled to write code such as:

Click here to view code image