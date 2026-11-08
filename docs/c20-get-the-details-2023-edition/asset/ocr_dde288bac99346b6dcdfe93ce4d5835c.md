```
40
41  }
```

Thanks to the header `<concepts>` in line 3, I can use the concept `std::integral`. The concept is fulfilled if T is integral[^10]. The function name gcd stands for the greatest-common-divisor algorithm based on the Euclidean[^11] algorithm.

Here are the four ways to use concepts:

+   - Requires clause (line 6)
+   - Trailing requires clause (line 13)
+   - Constrained template parameter (line 19)
+   - Abbreviated function template (line 25)

For simplicity reasons, each function template returns auto. There is a semantic difference between the function templates gcd, gcd1, gcd2, and the function gcd3. In the case of gcd, gcd1, or gcd2, arguments a and b must have the same type. This does not hold for the function gcd3. Parameters a and b can have different types but must both fulfill the concept `integral`.

```
gcd(100, 10) = 10
gcd1(100, 10) = 10
gcd2(100, 10) = 10
gcd3(100, 10) = 10
```

Use of the concept `std::integral`

The functions gcd and gcd1 use requires clauses. Requires clauses are more powerful than you may think. Let me discuss more details to requires clauses.

# 4.1.4.2 Requires Clause

The previous program, conceptsIntegralVariations.cpp, exemplifies that you can use a concept to define a function or function template. Of course, there are more use cases. For completeness, I want to add that you can specify the return type of a function or a function template using concepts.

The keyword requires introduces a requires clause that specifies constraints on a template argument (gcd) or on a function declaration (gcd1). Requires must be followed by a compile-time predicate, a named concept (gcd), or a requires expression. Of course, you can combine all of the three mentioned.

The compile-time predicate can also be an expression:

[^10]: https://en.cppreference.com/w/cpp/types/is_integral
[^11]: https://en.wikipedia.org/wiki/Euclid