
and entertainment services all contain C++ components. C++ services and applications are omnipresent in modern society. The reason is simple. The C++ language has progressed with its demands, and in many ways leads the innovations in programming productivity and execution efficiency. Both attributes make it the language of choice for applications that need to run at scale.

## Reasons to Learn C++

Like no other language, C++ masters the full spectrum from programming sufficiently close to the hardware on one end to abstract high-level programming on the other. The lower-level programming—like user-definable memory management—empowers you as a programmer to understand what really happens during execution, which in turn helps you understand the behavior of programs in other languages. In C++ you can write extremely efficient programs that can only be slightly outperformed by code written in machine language with ridiculous effort. However, you should wait a little with the hardcore performance tuning and focus first on clear and expressive software.

This is where the high-level features of C++ come into play. The language supports a wide variety of programming paradigms directly: object-oriented programming (Chapter 6), generic programming (Chapter 3), meta-programming (Chapter 5), concurrent programming (§4.6), and procedural programming (§1.5), among others.

Several programming techniques—like RAII (§2.4.2.1) and expression templates (§5.3)—were invented in and for C++. As the language is so expressive, it was often possible to establish these new techniques without changing the language. And who knows, maybe one day you will invent a new technique.

## Reasons to Read This Book

The material in the book has been tested on real humans. The author taught his class, “C++ for Scientists,” over three years (i.e., three times two semesters). The students, mostly from the mathematics department, plus some from the physics and engineering departments, often did not know C++ before the class were able to implement advanced techniques like expression templates (§5.3) by the end of the course. You can read this book at your own pace: straight to the point by following the main path or more thoroughly by reading additional examples and background information in Appendix A.

## The Beauty and the Beast

C++ programs can be written in so many ways. In this book, we will lead you smoothly to the more sophisticated styles. This requires the use of advanced features that might be intimidating at first but will become less so once you get used to them. Actually, high-level programming is not only more widely applicable but is usually equally or more efficient and readable.

We will give you a first impression with a simple example: gradient descent with constant step size. The principle is extremely simple: we compute the steepest descent of f(x) with its gradient, say g(x), and follow this direction with fixed-size steps to the next local minimum. Even the algorithmic pseudo-code is as simple as this description:

```
Algorithm 1: Gradient descent algorithm
Input: Start value x, step size s, termination criterion e, function f, gradient g
Output: Local minimum x
1 do
2 |x = x - s · g(x)
3 while |Δf(x)| >= e ;
```

For this simple algorithm, we wrote two quite different implementations. Please have a look and let it sink in without trying to understand the technical details.

Click here to view code image

```cpp
void
gradient_descent(double* x,
                 double* y, double s,
                 double eps,
                 double (*f)(double,
                             double),
                 double (*gx)(double,
                              double),
                 double (*gy)(double,
                              double))
{
    double val= f(*x, *y),
           delta;
    do {
        *x-= s * gx(*x,
                    *y);
        *y-= s * gy(*x,
                    *y);
        double new_val=
            f(*x, *y);
        delta= abs(new_val
                  - val);
        val= new_val;
    } while (delta > eps);
}
```

```cpp
template <typename Value,
          typename P1,
          typename P2,
          typename F,
          typename G>
Value gradient_descent(Value
                       x, P1 s,
                       P2 eps, F f, G g)
{
    auto val= f(x), delta=
        val;
    do {
        x-= s * g(x);
        auto new_val= f(x);
        delta= abs(new_val -
                   val);
        val= new_val;
    } while (delta > eps);
    return x;
}
```

At first glance, they look pretty similar, and we will tell you soon which one we like more. The first version is in principle pure C, i.e., compilable with a C compiler too. The benefit is that what is optimized is directly visible: a 2D function with `double` values (indicated by the **highlighted** function parameters). We prefer the second version as it is more widely usable: two functions of arbitrary dimension with arbitrary value types (visible by the **marked** type and function parameters). Surprisingly, the versatile implementation is not less efficient. To the contrary, the functions given for `F` and `G` may be inlined (see §1.5.3) so that the function call overhead is saved, whereas the explicit use of (ugly) function pointers in the first version makes this code acceleration difficult for the compiler.

A longer example comparing old and new styles is found in Appendix A (§A.1) for the really patient reader. There, the benefit of modern programming is much more evident than in the toy example here. But we do not want to hold you back too long with preliminary skirmishing.

## Languages in Science and Engineering

> "It would be nice if every kind of numeric software could be written in C++ without loss of efficiency, but unless something can be found that achieves this without compromising the C++-type system it may be preferable to rely on Fortran, assembler or architecture-specific extensions."
> 
> —Bjarne Stroustrup

Scientific and engineering software is written in different languages, and which one is the most appropriate depends on the goals and available resources:

- Math tools like MATLAB, Mathematica, or R are excellent when we can use their existing algorithms. When we implement our own algorithms with fine-grained (e.g., scalar) operations, we will experience a significant decrease in performance. This might not be an issue when the problems are small or the user is infinitely patient; otherwise we should consider alternative languages.
- Python is excellent for rapid software development and contains scientific libraries like "scipy" and "numpy," and applications based on these libraries (often implemented in C and C++) are reasonably efficient. Again, user-defined algorithms from fine-grained operations pay a performance penalty. Python is an excellent way to implement small and medium-sized tasks efficiently. When projects grow sufficiently large, it becomes increasingly important that the compiler is stricter (e.g., assignments are rejected when the argument types do not match).
- Fortran is also great when we can rely on existing, well-tuned operations like dense matrix operations. It is well suited to accomplishing old professors’ homework (because they only ask for what is easy in Fortran). Introducing new data structures is, in the author's experience, quite cumbersome, and writing a large simulation program in Fortran is quite a challenge—today only done voluntarily by a shrinking minority.
- C allows for good performance, and a large amount of software is written in C. The core language is relatively small and easy to learn. The challenge is to write large and bug-free software with the simple and dangerous language features, especially pointers (§1.8.2) and macros (§1.9.2.1). The last standard was released in 2017 and thus is named C17. Most C features—but not all—were sooner or later introduced into C++.
- Languages like Java, C#, and PHP are probably good choices when the main component of the application is a web or graphic interface and not too many calculations are performed.
- C++ shines particularly when we develop large, high-quality software with good performance. Nonetheless, the development process does not need to be slow and painful. With the right abstractions at hand, we can write C++ programs quite rapidly. We are optimistic that in future C++ standards, more scientific libraries will be included.

Evidently, the more languages we know, the more choice we have. Moreover, the better we know those languages, the more educated our choice will be. In addition, large projects often contain components in different languages, whereas in most cases at least the performance-critical kernels are realized in C or C++. All this said, learning C++ is an intriguing journey, and having a deep understanding of it will make you a great programmer in any case.

## Typographical Conventions

New terms are set in clear blue and italic. C++ sources are printed blue and monospace. Important details are marked in boldface. Classes, functions, variables, and constants are lowercase, optionally containing underscores. An exception is matrices, which are usually named with a single capital letter. Template parameters and concepts start with a capital letter and may
