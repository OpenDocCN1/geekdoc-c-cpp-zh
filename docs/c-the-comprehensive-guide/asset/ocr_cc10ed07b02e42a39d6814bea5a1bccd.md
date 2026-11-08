# Avoiding Recursion with “constexpr-if”

With C++17, you can simplify code with multiple specialized function templates into a single general function template. You do this with if constexpr(...): The condition specified in parentheses must be evaluable at compile time. You can then combine the first three helper definitions from the previous example as in the following listing.

```
```cpp
// https://godbolt.org/z/KvsGh4f1v
namespace lits {
    // Template helper function for one argument
    template<char C> int bin() {  // general case
        if constexpr (C=='0') return 0;
        else if constexpr (C=='1') return 1;
    }
    // Template helper function for two or more arguments
    // ...
}
```
```

**Listing 23.40**  The new if constexpr saves function specializations.

The C==0 and C==1 expressions are evaluable at translation time. bin<'0'> and bin<'1'> can therefore be computed by the compiler.

The special thing about this constexpr-if is that it behaves as if you had written different template specializations: code from then branches that you never need in the entire program is not instantiated by the compiler. It does not appear in the translated program and does not affect its size or runtime.

# With Fold Expressions to One-Liners

Admittedly, the recursive template definition from Listing 23.39 is not easy to digest. Such constructs with helper templates and partial specializations have been a thing of the past since C++17. I just want to give a small insight into fold expressions, which will simplify a lot in the implementation of variadic templates.

The implementation in Listing 23.41 only converts the literal into a string that looks exactly like the literal.

```
```cpp
// https://godbolt.org/z/cPoEjgZM7
#include <iostream>
#include <string>
namespace lits {
    // operator""_sx
    template<char... CS> std::string operator""_sx() {
        return (std::string{} + ... + CS); // a fold expression
    }
}
```
```