# 3. Lambdas in C++14

C++14 added two significant enhancements to lambda expressions:

+   - Captures with an initialiser
- Generic lambdas

Plus, the Standard also updated some rules, for example:

+   - Default parameters for lambdas
- Return type as auto

These features can solve several issues that were visible in C++11.

You can see the specification in N4140 and lambdas: [expr.prim.lambda].

What’s more, in this chapter, you’ll learn about:

+   - Capturing member variables
- Replacing old functional stuff like std::bindist with modern techniques
- LIFTING
- Recursive Lambdas