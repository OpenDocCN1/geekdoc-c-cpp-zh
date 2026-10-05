```
std::ranges::sort(data);
}
```

Here you use an abbreviated function template via auto together with the concept random_access_range. Note that when using ranges as parameters, you should typically use the universal reference &&.

# Universal References

When you write operations yourself, they will receive parameters as rvalue references &&. When you mix this && syntax with templates, you need to be aware of one thing: the && parameter is not necessarily an rvalue reference, as I explained in Chapter 23.

Normally, you want to forward the && parameter in a template only via std::forward to another function (and nothing more). Or if you wanted something entirely different, then && for the template parameter was probably wrong and do not do what you intended.

# Relevant Guidelines

+   - T.1: Use templates to raise the level of abstraction of code.
- T.2: Use templates to express algorithms that apply to many argument types.
- T.3: Use templates to express containers and ranges.
- T.40: Use function objects to pass operations to algorithms. [A function object can carry more]