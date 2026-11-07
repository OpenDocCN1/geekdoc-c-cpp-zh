ond digit in this example) to the nearest even integer. So with `cpp_dec_float_50`, the value 1157.625 rounds down to 1157.62. Similarly,

+   - 1157.635 would round up to 1157.64,
+   - 1157.645 would round down to 1157.64,
+   - 1157.655 would round up to 1157.66,
+   - 1157.665 would round down to 1157.66,
+   - etc.

# 4.15 Wrap-Up

In this chapter, we completed our introduction to all but one of C++’s control statements, which enable you to control the flow of execution in functions. Chapter 3 discussed `if`, `if...else` and `while`. Chapter 4 demonstrated `for`, `do...while` and `switch`. We introduced C++20’s new text formatting from the `<format>` header.

We showed initializing a variable in the header of an `if` and `switch` statement. You used the `break` statement to exit a `switch` statement and to terminate a loop immediately. You used a `continue` statement to terminate a loop’s current iteration and proceed with the loop’s next iteration, and we mentioned that `while` and `do...while` loops proceed immediately to their loop-continuation conditions, whereas `for` loops proceed to their increments first. We introduced C++’s logical operators for creating more complex conditional expressions in control statements.

In our first compound-interest example, we discussed the representational errors associated with floating-point types. Then, in the Objects-Natural case study, we performed precise monetary calculations using the Boost Multiprecision library’s predefined class `cpp_dec_float_50` for representing floating-point numbers exactly and performing “to-the-penny” arithmetic. We showed that built-in type `double` uses the biased half-up rounding algorithm and that `cpp_dec_float_50` eliminates that bias by using banker’s rounding.

In Chapter 5, you’ll create your own custom functions, learn simulation techniques with random-number generation, use function templates to define families of functions that perform the same tasks or different types, be introduced to private-key encryption, and more.

# Exercises

+   4.1 Describe the four basic elements of counter-controlled iteration.
+   4.2 Compare and contrast the `while` and `for` iteration statements.
+   4.3 Discuss a situation in which it would be more appropriate to use a `do...while` statement than a `while` statement. Explain why.
+   4.4 Compare and contrast the `break` and `continue` statements.

11. “Rounding,” Wikipedia. Wikimedia Foundation. Accessed April 14, 2023. https://en.wikipedia.org/wiki/Rounding.