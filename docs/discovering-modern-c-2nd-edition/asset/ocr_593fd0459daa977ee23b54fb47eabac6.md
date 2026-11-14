+   - Avoid names of popular macros. Most prominently, `assert` is a macro in the standard library and giving that name to a function is asking for trouble.
+   - Un-define the macro with colliding names using `#undef`.
+   - Include macro-heavy libraries after all others. Then the macros still pollute your application but not the other included header files.
+   - Impressively, some libraries offer protection against their own macros: one can define a macro that disables or renames macros’ dangerously short names.²

2. We have seen a library that defined a single underscore as a macro, which created a lot of problems.

# A.3 Real-World Example: Matrix Inversion

To round up the basic features, we apply them to demonstrating how we can easily create new functionality. We want to give you an impression of how our ideas can evolve naturally into reliable and efficient C++ programs. Particular attention is paid to clarity and reusability. Our programs should be well-structured inside and intuitive to use from outside.

To simplify the realization of our study case, we use (the open-source part of) the author’s library *Matrix Template Library* ⁴—see `http://www.mtl4.org`. It already contains a lot of linear-algebra functionality that we need here.³ We hope that future C++ standards will provide a similar linear-algebra library. Maybe some of the readers will contribute to it.

3. It actually already contains the inversion function `inv` we are going for, but let us pretend it does not.

As a software development approach, we will use a principle from *Extreme Programming*: writing tests first and implementing the functionality afterward—known as *Test-Driven Development* (TDD). This has several significant advantages: