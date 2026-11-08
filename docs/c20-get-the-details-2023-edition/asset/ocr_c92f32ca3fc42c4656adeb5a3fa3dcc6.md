# # Compile-Time Regular Expressions

A very impressive use-case for string literals is compile-time parsing of regular expressions[^1]. There is already a proposal for C++23 in the pipeline: P1433R0: Compile-Time Regular Expressions[^2]. Hana Dusíková as the author of the proposal motivates compile-time regular expressions in C++: "*The current std::regex design and implementation [regular expression library] are slow, mostly because the RE [regular expression] pattern is parsed and compiled at run time. Users often don't need a runtime RE [regular expression] parser engine as the pattern is known during compilation in many common use cases. I think this breaks C++'s promise of 'don't pay for what you don't use'.*"

*If the RE [regular expression] is known at compile time, the pattern should be checked during the compilation. The design of std::regex doesn't allow for this[compile-time evaluation,] as the RE input is a run-time string and syntax errors are reported as exceptions[^3].*

# # Distilled Information

+   - A conditionally explicit constructor allows it to control explicitly for a generic constructor which types can be used in a constructor.
+   - C++20 supports further floating-point types, literal types, and string literals as non-type template parameters.

[^1]: https://github.com/hanickadot/compile-time-regular-expressions
[^2]: https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1433r0.pdf
[^3]: https://en.cppreference.com/w/cpp/regex