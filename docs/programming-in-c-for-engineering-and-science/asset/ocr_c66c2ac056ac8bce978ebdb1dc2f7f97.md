# 6.5 INTRODUCTION TO NUMERICAL METHODS

Problems and mathematical models in science and engineering, plus a wide variety of other areas, involve solving ordinary algebraic equations, differential equations, systems of equations, and so on. In many cases, numerical methods that can be implemented by computer programs are used to find solutions. Here are some of the major types of problems in which numerical methods are routinely used:

+   1. For a few algebraic equations, a formula (e.g., the quadratic formula for quadratic equations) gives the exact roots, but for most equations, a numerical method is used to find approximate roots.
+   2. The solution of many problems such as finding the area under a curve, calculating probabilities of certain events, and calculating work done by a force, require the evaluation of an integral. For some, the methods of integral calculus can be used, but for others a numerical technique is used to find approximate values.
+   3. Differential equations play an important role in many applications, and a variety of effective and efficient numerical methods have been developed to obtain solutions.
+   4. Curve fitting refers to analyzing pairs of data values to determine whether the items in these pairs are related by some algebraic equation. For example, the least-squares method described in Programming Problem 10 of Section 9.4 is a method for fitting a line to a set of points.
+   5. Numerical methods are commonly used to find a collection of values that satisfies a collection of linear equations with several unknowns simultaneously. Such linear systems will be described later when we consider matrices.

In this section, a few of the numerical methods in the first three categories are described.

# 6.5.1 Solving Equations—The Bisection Method

In many applications it is necessary to find a zero or root of a function, that is, to solve an equation of the form f(x) = 0. For some functions it may be very difficult or even impossible to find this solution exactly. Examples include the function

```
f(v) = 50·10⁻⁹ (e⁴⁰ᵛ − 1) + v − 20
```

which may arise in a problem of determining the d-c operating point in an electrical circuit, or a function of the form

```
f(x) = x tan x − a
```