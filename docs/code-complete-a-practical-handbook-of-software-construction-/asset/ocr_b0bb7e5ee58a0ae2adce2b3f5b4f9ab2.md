# 26.4 Expressions

Cross-Reference For more information on expressions, see Section 19.1, "Boolean Expressions."

Much of the work in a program is done inside mathematical or logical expressions. Complicated expressions tend to be expensive, so this section looks at ways to make them cheaper.

# Exploit Algebraic Identities

You can use algebraic identities to replace costly operations with cheaper ones. For example, the following expressions are logically equivalent:

```
not a and not b
not (a or b)
```

If you choose the second expression instead of the first, you can save a not operation.

Although the savings from avoiding a single not operation are probably inconsequential, the general principle is powerful. Jon Bentley describes a program that tested whether sqrt(x) < sqrt(y) (1982). Since sqrt(x) is less than sqrt(y) only when x is less than y, you can replace the first test with x < y. Given the cost of the sqrt() routine, you’d expect the savings to be dramatic, and they are. Here are the results:

| Language | Straight Time | Code-Tuned Time | Time Savings | Performance Ratio |
|---|---|---|---|---|
| C++ | 7.43 | 0.010 | 99.9% | 750:1 |
| Visual Basic | 4.59 | 0.220 | 95% | 20:1 |
| Python | 4.21 | 0.401 | 90% | 10:1 |

# Use Strength Reduction

As mentioned earlier, strength reduction means replacing an expensive operation with a cheaper one. Here are some possible substitutions:

+   - Replace multiplication with addition.
+   - Replace exponentiation with multiplication.
+   - Replace trigonometric routines with their trigonometric identities.
+   - Replace longlong integers with longs or ints (but watch for performance issues associated with using native-length vs. non-native-length integers)
+   - Replace floating-point numbers with fixed-point numbers or integers.
+   - Replace double-precision floating points with single-precision numbers.
+   - Replace integer multiplication-by-two and division-by-two with shift operations.