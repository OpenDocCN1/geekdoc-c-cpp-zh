in namespace blocks if you don't want to. You can instead tie the definitions to their declarations by qualifying the function names with the correct namespace names in their definitions. This is illustrated by options 3 and 4 in math.cpp.

It goes without saying that mixing all these different options is not considered good style (and certainly not within one file). Instead, you should pick one option (most commonly option 1 or 3 in math.cpp) and then consistently use that style for all your function definitions.

# ## Using Directives and Declarations

From Chapter 3 you already know that by using a blanker as using directive you can reference any name from a namespace without qualifying it with the namespace name:

```
    using namespace std;
```

However, this risks defeating the purpose of using namespaces in the first place and increases the likelihood of errors because of the accidental use of a name in the std namespace. It is thus often better to use qualified names or add using declarations for the names from another namespace that you are referencing. A using declaration, as you also know from Chapter 3, allows you to use a specific name without its namespace qualification. Here are some examples:

```
    using std::vector;
    using std::max;
```

These declarations introduce the names vector and max from the namespace std into the current scope or namespace. One using declaration may introduce many different entities. For instance, the using directive for std::max introduces all possible instantiations and overloads of the various std::max() templates with a single using declaration.

We have occasionally placed some using declarations and directives already at global scope in some examples. But you can also place them within a namespace, within a function, or even within a statement block. When placed in a namespace, it makes a name from one namespace available within another. Here is a variation of Ex11_068 that uses this technique:

```
    // squaring.cppm
    module; // Start of the global module fragment (for #include directives)
    #include <cmath> // For std::sqrt()
    export module squaring;
    import <numbers>; // For std::numbers::sqrt2

    export namespace math
    {
        using std::numbers::sqrt2;
        using std::sqrt; // Never 'using std::sqrt();' or 'using std::sqrt(double);'!
        auto square(const auto& x) { return x * x; }
        auto pow(const auto& x) { return square(square(x)); }
    }
```

By adding the using std::numbers::sqrt2; declaration, you ensure that by importing squaring you can qualify the sqrt2 constant both as std::numbers::sqrt2 and math::sqrt2. Note that if the entire math namespace was not exported already, you would have to use export using std::numbers::sqrt2; to make this alias visible from outside the squaring module.