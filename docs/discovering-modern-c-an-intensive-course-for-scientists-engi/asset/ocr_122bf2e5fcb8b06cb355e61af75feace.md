# ## 3.5 A Bit of Theory on Templates: Concepts

> > "Gray, dear friend, is all theory and green the life's golden tree."<sup>8</sup>
> > —Johann Wolfgang von Goethe

In the previous sections, you might have gotten the impression that template parameters can be substituted by any type. This is in fact not entirely true. The programmer of template classes and functions makes assumptions about the operations that can be performed on the template arguments.

Thus, it is very important to know which argument types are acceptable. We have seen, for instance, that `accumulable` can be instantiated with `int` or `double`. Types without addition like a solver class (on page 74) cannot be used for `accumulable`. What should be accumulated from a set of solvers? All the requirements for the template parameter `T` of function `accumulate` can be summarized as follows:

+   - `T` is copy-constructible: `T a(b);` is compilable when the type of `b` is `T`.
+   - `T` is plus-assignable: `a+= b;` compiles when the type of `a` and `b` is `T`.
+   - `T` can be constructed from `int`: `T a(0);` compiles.

Such a set of type requirements is called a _Concept_. A concept `C` that contains all requirements of concept `C` and possibly additional requirements is called a _Refinement_ of `C`. A type `T` that holds all requirements of concept `C` is called a _Model_ of `C`. Plus-assignable types are, for instance, `int`, `float`, `double`, and even `string`.

A complete definition of a template function or class should contain the list of required concepts as is done for functions from the Standard Template Library; see `http://www.sgi.com/tech/stl/`.

Today such requirements are only documentation. Future C++ standards will most likely support concepts as a central language feature. A technical specification mainly by Andrew Sutton, "C++ Extensions for Concepts," [46] is in progress and may be part of C++17.

# ## 3.6 Template Specialization

On one hand, it is a great advantage that we can use the same implementation for many arguments types. For some argument types we may, however, know a more efficient implementation, and this can be realized in C++ with _Template Specialization_. In principle, we could even implement an entirely different behavior for certain types at the price of utter confusion. Thus, the specialization will be more efficient but behave the same. C++ provides enormous flexibility, and we as programmers are in charge of using this flexibility responsibly and of being consistent with ourselves.