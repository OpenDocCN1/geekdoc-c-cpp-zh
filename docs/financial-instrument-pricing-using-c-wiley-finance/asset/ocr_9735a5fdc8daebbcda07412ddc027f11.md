# CHAPTER 4

# Advanced C++ Template Programming

# 4.1 INTRODUCTION AND OBJECTIVES

This chapter introduces a number of new and advanced language features in C++. These features underlie much of *template metaprogramming* that is making its way into the standard (Abrahams and Gurtovoy, 2005). We give a detailed analysis of these features in this chapter and continue on the same theme in Chapter 6.

The goals of this chapter are:

+   - To acquaint the reader with template metaprogramming (TMP) in C++.
+   - To give illustrative examples of TMP to show its application to creating robust code.
+   - To discuss how to use TMP in your applications.

This chapter can be skipped on a first reading. It can be used mainly as reference for a specific syntax. As with Chapter 6, the topics in this chapter are probably more useful to library builders than to application programmers.

Central to metaprogramming is the concept of a metafunction. In general terms, a *metafunction* is the compile-time analogue of a run-time function. Traditional functions accept values/objects as parameters and return values or objects. However, metafunctions accept types and compile-time constants as parameters and return types and constants. Metafunctions can be used to implement the following functionality:

+   - Encapsulate a complex type computational algorithm.
+   - Generate a type using compile-time type selection techniques.

A metafunction is a template. In general, *metafunction implementation* is usually based on template specialisation. We take an example of a metafunction that computes *Fibonacci numbers* {F_n}_{n ≥ 0} given by the iterative algorithm:

F₀ = 0
F₁ = 1
Fₙ = Fₙ₋₁ + Fₙ₋₂,   n ≥ 2.