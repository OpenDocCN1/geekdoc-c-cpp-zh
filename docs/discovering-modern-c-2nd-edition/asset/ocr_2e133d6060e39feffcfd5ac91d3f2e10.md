```
template <typename Matrix>
inline auto frobenius_norm(const Matrix& A)
{
    using std::abs; using std::sqrt;
    decltype(abs(A[0][0])) ss = 0;
    on_each_nonzero(A, [&ss](auto x) { ss+= abs(x) * abs(x);
    }));
    return sqrt(ss);
}
```

In this little function, we used more type deduction mechanisms and liberated ourselves entirely from declaring `value_type`. We can now also handle the fact that `abs` might return a type different from `value_type`. C++17 C++20 C++17 allows us to define lambdas that are evaluated at compile time. We will discuss them in Section 5.1.5 once we talk about compile-time computation at large. C++20 also named template parameters as for regular function templates. This allows us for instance to write generic lambdas requiring that multiple parameters must be instantiated to the same type. And some lambdas with type deduction might be written more concisely. In face of this expressive power that still increases:

# Advice

Use lambdas with moderation! Not everything that is doable with lambdas needs to be done with them. Use them to make your programs more expressive not more obscure.

Avoid endless and overly complicated lambdas. Even in modern C++, a traditional function or class might be a better choice for the overall clarity. The author's personal guideline is:

+   - Create a lambda in a function call if the call still fits in one line and the lambda is used only once.
+   - Split nested lambdas and store at least the inner lambdas.
+   - Store a lambda in a variable if it is no longer than five lines.
+   - Everything beyond this is better implemented in another fashion.