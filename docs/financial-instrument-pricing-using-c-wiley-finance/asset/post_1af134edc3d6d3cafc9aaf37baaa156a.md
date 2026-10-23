
where $|\Sigma|$ is the determinant of the $n \times n$ covariance matrix defined by:

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_856_0.png)

Here $\Sigma^{-1}$ is the inverse of $\Sigma$. Furthermore, $x$ and $\mu$ are $n$-dimensional vectors. A special case is the standard $n$-dimensional normal $N(0,I_n)$ having the form

$$\frac{1}{(2\pi)^{n/2}}\exp\left(-\frac{1}{2}x^Tx\right)$$

where $x^T$ is the transpose of the vector $x$. Here $I_n$ is the $n \times n$ identity matrix.

We note that the symmetric matrix $\Sigma$ is positive definite, that is $x^T\Sigma x > 0\ \forall x \in \mathbb{R}^n$ and we can express it in Cholesky decomposition form, namely $\Sigma = CC^T$ where $C$ is a lower-triangular matrix.

The objective of this exercise is to generate a correlated vector $X$. We describe the steps to execute the algorithm.

+   Answer the following questions:
+   
+    a) Generate an uncorrelated $N(0,1)$ vector $Z$.
+   
+    b) Calculate the Cholesky lower-triangular matrix $C$.
+   
+    c) Compute the new correlated random vector $X = CZ + m$ where $m$ is the mean of $X$.

Implement a solution in C++11 in combination with a matrix library, such as *Eigen*, *Boost uBLAS* or your own favourite library.

## 7. (Laplace Distribution)

Even though C++ does not support all univariate distributions that does not mean all is lost! In some cases we may be able to generate random numbers from a given distribution if we have an analytic form for its cdf, for example. More specifically, we may be able to invert the cdf and then we are done or failing that we can use the Newton–Raphson method or the fixed-point method to iteratively compute the solution. In this exercise we concentrate on the analytic approach by examining the *Laplace* and *Extreme Value* distributions, the latter being supported in C++11.

The *Laplace distribution* (also called the *double exponential distribution*) can be seen as the difference between two independent identically distributed exponential random variables. It depends on a *location parameter* $\mu$ and a *scale (diversity) parameter* $b \ge 0$. In the case $\mu = 0$ and $b = 1$ we get an exponential distribution on the positive half-line scaled by a factor $1/2$. The pdf and cdf for the Laplace distribution are given respectively by:

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_856_1.png)

Prove that a random variate of this distribution is given by:

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_856_2.png)

where U is drawn from a uniform distribution in the interval (−1/2, 1/2).

The second example is the Extreme Value distribution whose pdf and cdf are given respectively by:

$f(x) = \sigma^{-1} \exp\left(-\frac{x - \mu}{\sigma}\right) \exp\left(-\exp\left(-\frac{x - \mu}{\sigma}\right)\right), \ x \in \mathbb{R}$

$F(x) = \exp\left(-\exp\left(-\frac{x - \mu}{\sigma}\right)\right), \ x \in \mathbb{R}.$

Show that:

$X = -\sigma \log(-\log(U)) + \mu$

where U is drawn from a uniform distribution in the interval (0, 1). In the case of the extreme value distribution compare your results with those from C++11.

Write functions in C++ to compute random variates from these two distributions.

## 8. (A Reusable Framework for Random Number Generation)

The goal of this exercise is to create a software framework containing functionality that is needed for random number generation in computational finance. We focus on producing arrays of correlated random numbers. The main requirements are efficiency and accuracy in the short term and then extendibility in a second increment of the framework. You should use the generic class RNGgenerator from Section 15.5.2 as it contains functionality that you can use in the framework.

Answer the following questions:
a) Extend the functionality of RNGgenerator for the creation of matrices with random values.
b) Create free functions to generate two correlated standard normal variates having a given correlation.
c) Create two separate functions to generate an array of correlated random numbers using Cholesky decomposition; one function uses the code presented in Section 26.9.1 while the second function uses the Eigen library. Test these functions on examples to compare efficiency and accuracy. Does Eigen support Cholesky decomposition on matrices with complex coefficients?
d) Stress test: create a loop and in the loop create a random covariance matrix. Apply the functions from part c). Compute the maximum error between the two solutions.
e) Modify the code so that it can switch between different implementations of the Cholesky algorithm (we are typically thinking of a Strategy design pattern (GOF, 1995) or a mixin). Implement this code using the CRTP with std::function as embedded algorithm.
f) Can you discover new requirements and features that you would like to add to the software framework?

# CHAPTER 27

# Microsoft .Net, C# and C++11 Interoperability

## 27.1 INTRODUCTION AND OBJECTIVES

In this chapter we introduce the C++/CLI (Common Language Infrastructure) language. It is a .NET programming language similar to C# and VB.NET in terms of efficiency and functionality but with the added advantage that it is possible to write applications containing a mixture of C++/CLI, C# and native C++ code.

Before we discuss the C++/CLI language we give an overview of the programming knowledge and skills that are needed in order to become comfortable with the language. In particular, it is especially important to understand the similarities and differences between native C++ and C++/CLI (and to a lesser extent between C# and C++/CLI). Ideally, a good working knowledge of C++ is a prerequisite in order to understand C++/CLI, including pointers, memory management, classes and templates. C++/CLI code can be mixed with native C++ code. It is important to distinguish between the two languages and this is achieved by having a good knowledge of each one. Furthermore, C++/CLI is relatively easy to learn for developers who already program in C#. Since C# and C++/CLI are both .NET languages they share a common syntax. Programs that have been written in C# are easily understood by developers who know C++/CLI and it is not too difficult for C# developers to fathom C++/CLI.

We summarise the goals and content in this chapter:

- A global overview of the .NET language C++/CLI.
- Memory management in .NET.
- The various ways to create multi-language (C#, C++ and C++/CLI) applications.
- Using C++ libraries (for example, Boost and Quantlib) in .NET applications.
- Next-generation Observer design pattern (using .NET Events) and using it in native C++.
- Integration with legacy C, native C++ and COM code.
- .NET assemblies and their integration with our software framework as introduced in Chapter 9.

We are unable to discuss everything that we would like to discuss due to lack of space. However, we are working on a follow-up text in which we expand on these interoperability topics.

## 27.2 THE BIG PICTURE

C++/CLI differs from C++ in a number of ways. Some of the differences are related to the fact that C++/CLI is a .NET language and it enjoys many features that are not supported in C++:

- a) It is a dynamic language and it has support for introspection (Reflection), dynamic loading of assemblies (dlls) and dynamic object creation.
- b) Access to .NET libraries for databases, serialisation, networking, graphical user interfaces and web services, for example.
- c) Support for multithreading and parallel programming.
- d) Automatic memory management and garbage collection support.
- e) Support for interfaces.
- f) Support for delegates and events.
- g) Support for properties (standardised getters and setters for member data).

Part of the challenge when learning C++/CLI is to know which features in native C++ do and do not work in that language and how the two languages cooperate together. They have much in common but there are differences.

C++/CLI is a set of extensions to C++ to benefit from the services that an implementation of the CLI offers. It is a .NET language and you will find it easy to learn if you know (native) C++ and some C#. In particular, you can freely mix C++/CLI and C++ code in a project and in this sense we say that C++/CLI is bilingual because it can talk to both .NET code and native C++ code. A summary of the language from Wikipedia reads:

> C++/CLI (C++ modified for CLI) is a language specification created by Microsoft and intended to supersede Managed Extensions for C++. It is a complete revision that aims to simplify the older Managed C++ syntax, which is now deprecated. C++/CLI was standardised by Ecma as ECMA-372. It is currently available in Visual Studio 2005, 2008, 2010, 2012, 2013, 2015 and 2017, including the Express editions.

As already mentioned, the syntax of C++/CLI will be easy to learn if you already know C#. An added advantage is knowledge of (native) C++. There are a number of differences between C++ and C++/CLI, however, one of which is the memory model in .NET. Objects are of course instances of classes and they are always created on the heap in .NET (unless we define value types). This is different from C++ where objects can also be created on the stack. Objects are automatically garbage collected in C++/CLI. In contrast, value types’ values live on the stack and are not garbage collected. It is important to distinguish between value types and reference types in .NET as these can be a source of confusion. By default, all classes are derived from System::Object, which is the lowest common denominator of almost all .NET types. This base class can refer to any kind of object or value and its data lives on the heap. We need to discuss how to convert values to objects (boxing) and convert objects to values (unboxing). A simple example is:

```
int i = 42;
Object^ obj = (Object^)i;                  // boxing
Console::WriteLine("Values: {0}", obj->ToString());   // 42
```
