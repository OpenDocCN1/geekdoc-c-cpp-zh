# Section 6.12 Inline Functions

+   - C++ provides **inline functions** (p. 241) to help reduce function-call overhead—especially for small functions. Placing the qualifier `inline` (p. 241) before a function’s return type in the function definition advises the compiler to generate a copy of the function’s code in every place that the function is called to avoid a function call.
+   - Compilers can inline code for which you have not explicitly used the `inline` keyword. Today’s optimizing compilers are so sophisticated that it’s best to leave inlining decisions to the compiler.