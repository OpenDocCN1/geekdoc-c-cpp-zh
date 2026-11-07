# # Outline

+   - 4.1 Introduction
+   - 4.2 Essentials of Counter-Controlled Iteration
+   - 4.3 for Iteration Statement
+   - 4.4 Examples Using the for Statement
+   - 4.5 Application: Summing Even Integers; Introducing C++20 Text Formatting
+   - 4.6 Application: Compound-Interest Calculations; Introducing Format Specifiers
+   - 4.7 do...while Iteration Statement
+   - 4.8 switch Multiple-Selection Statement
+   - 4.9 Selection Statements with Initializers
+   - 4.10 break and continue Statements
+   - 4.11 Logical Operators
+     - 4.11.1 Logical AND (&&) Operator
+     - 4.11.2 Logical OR (||) Operator
+     - 4.11.3 Short-Circuit Evaluation
+     - 4.11.4 Logical Negation (!) Operator
+     - 4.11.5 Example: Producing Logical-Operator Truth Tables
+   - 4.12 Confusing the Equality (==) and Assignment (=) Operators
+   - 4.13 Structured-Programming Summary
+   - 4.14 Objects Natural Case Study: Precise Monetary Calculations with the Boost Multiprecision Library
+   - 4.15 Wrap-Up
+   - Exercises

# ## 4.1 Introduction

This chapter continues our presentation of structured-programming theory and principles by introducing all but one of C++'s remaining control statements—for, do...while, switch, break and continue. We explore the essentials of counter-controlled iteration. We use compound-interest calculations to begin investigating the issues of processing monetary amounts and the representational errors associated with floating-point types.

We use a switch statement to count the number of A, B, C, D and F grade equivalents in a set of numeric grades. We show if and switch statements capabilities that allow you to initialize one or more variables in these statements' headers. We discuss the logical operators, which enable you to combine simple conditions to form compound conditions. We also summarize C++'s control statements and the proven problem-solving techniques presented in this chapter and Chapter 3.

We introduce C++20's powerful and expressive text-formatting capabilities, which are based on those in Python, Microsoft's .NET languages (like C# and Visual Basic) and Rust.¹ The C++20 capabilities are more concise and powerful than those in earlier C++ versions.

We discuss the challenges of processing monetary amounts with floating-point types like double. Then, in Section 4.14's Objects Natural Case Study, we represent and manipulate monetary amounts precisely using objects of a class from the Boost Multiprecision Library. You'll see that the class provides the same mathematical capabilities as built-in numeric types, making it convenient to use.

# ## 4.2 Essentials of Counter-Controlled Iteration

Let's use the while iteration statement (Section 3.7) to formalize the elements of counter-controlled iteration:

+   1. a control variable (or loop counter)

1. Victor Zverovich, “Text Formatting,” July 16, 2019. Accessed April 14, 2023, http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p0645r10.html.