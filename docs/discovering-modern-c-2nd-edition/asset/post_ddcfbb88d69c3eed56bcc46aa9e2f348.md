
expression templates. That allows us to write extremely efficient scientific programs in a notationally convenient manner. With the techniques from this section we are now able to write large expressions without risking stale references. Expression templates in large projects cause quite some development effort and we tried to keep it simple to start you off. The classes can be significantly improved by incorporating the domain-specific type traits like `is_vector` from the preceding section to ascertain that the template arguments are instantiated with appropriate types. With sufficient C++20 compiler support it is highly recommendable to use concept constraints instead of enable-if constructs.

## C++17 5.4 Meta-Tuning: Write Your Own Compiler Optimization

Introductory remark: This section is marked as a C++17 implementation. However, the techniques themselves are feasible with older standards as well. We actually worked on this already with C++03 and such codes are still present in MTL4. Using C++17 allows us to realize special cases with `constexpr-if` instead of template specialization. You can find those codes in the GitHub examples when you look for sources with the same name in the `c++11` or `c++03` directory. The C++11 examples can be easily transformed into C++03. C++11 is primarily used to benchmark the codes with the `<chrono>` library. The older implementations also used the call operator whereas we now take a static function for saving the object creation (and the `nullptr` test of the `this` pointer).

Compiler technology is progressing, and more and more optimization techniques are provided. Ideally, we all write software in the easiest and most readable way, and the compiler generates the optimal executable out of it. We would only need a newer and better compiler for our programs to become faster and faster. Unfortunately, this only sometimes works.

In addition to general-purpose optimizations like copy elision (§2.3.5.3), compilers provide numeric optimization techniques like `Loop Unrolling`: the loop is transformed such that multiple iterations are performed in each iteration. This decreases the overhead of loop control and increases the potential for concurrent execution. Many compilers apply this technique only on the inner loop whereas unrolling multiple loops often enables even better performance. Several iterative calculations benefit from the introduction of additional temporaries which in turn can require semantic information that is not available for user types or operations.

Some compilers are particularly tuned for specific operations— especially those used in benchmarks and even more specifically for the LINPACK benchmark used to rate the 500 fastest computers in the world (www.top500.org). For instance, they can use pattern matching to recognize the typical three-nested loop in canonical dense-matrix multiplication and replace this code with a highly tuned assembler implementation that can be one or more orders of magnitude faster. These programs use seven or nine loops with platform-dependent block size to squeeze out the last bit of every cache level, transpose sub-matrices, run on multiple threads, perform a filigree register choreography, and so on.8

8. One could sometimes get the impression that the High-Performance Computing (HPC) community believes that multiplying dense matrices at near-peak performance solves all performance issues of the world or at least demonstrates that everything can be computed at near-peak performance if only one tries hard enough. Fortunately, more and more people in the supercomputer centers realize that their machines are not only running dense-matrix operations and that real-world applications are in most cases limited by memory bandwidth and latency.

Having a simple loop implementation replaced with code running at almost peak performance is definitely a great achievement. Unfortunately, this makes many programmers believe that most calculations can be similarly accelerated. Often small changes suffice to fall out of the pattern and the performance is much less spectacular than expected. No matter how generally the patterns are defined, their applicability will always be limited. An algorithmic change (e.g., multiplying triangular instead of rectangular matrices) that does not impede the blocking and unrolling optimizations will probably fall out of the compiler's special-case optimization.

To make a long story short: compilers can do a lot but not everything. Regardless of how many special cases are tuned by a compiler, there will always be a need for domain-specific optimizations. Alternatively to the techniques in compilers, there are tools like ROSE [53] that allow you to transform source code (including C++) with user-defined transformations on the abstract syntax tree (AST, the compiler-internal representation of programs).

A major roadblock for compiler optimization is that certain transformations require semantic knowledge. This is only available for types and operations known to the compiler implementers. The interested reader might also look at a deeper discussion of the topic in [22]. Research is going on to provide user-defined transformations with concept-based optimization [67]. Unfortunately, it will take time for this to become mainstream; even the new Concept extension introduced in C++20 is only a step toward optimization driven by user semantics since it will only deal with syntax at first and semantic concepts can only be emulated (see §5.5).

In the next two sections, we will show user-defined code transformations with meta-programming in the domain of linear algebra. The goal is that the user writes operations as clearly as possible and the function and class templates reach for the maximal achievable performance. Given the Turing completeness of the template system, we can provide any desirable user interface while realizing an implementation underneath that behaves equivalently to the most efficient code, as we will demonstrate in this section. Writing well-tuned templates is a significant programming, testing, and benchmarking effort. For this to pay off, the templates should be contained in well-maintained libraries that are available to a broad user community (at least within the research team or company).

### 5.4.1 Classical Fixed-Size Unrolling

```
=> c++17/fsize_unroll_test.cpp
```

The easiest form of compile-time optimization can be realized for fixed-size data types, in particular for math vectors like those in Section 3.6. Similar to the default assignment, we can write a generic vector assignment:

Click here to view code image

```cpp
template <typename T, int Size>
class fsize_vector
{
public:
    const static int my_size= Size;
    template <typename Vector>
    self& operator=(const Vector& that)
    {
        for (int i= 0; i < my_size; ++i)
            data[i]= that[i];
    }
};
```

A state-of-the-art compiler will recognize that all iterations are independent from each other; e.g., data[2]= that[2]; is independent of data[1]= that[1];. The compiler will also determine the size of the loop during compilation. As a consequence, the generated binary for an fsize_vector of size 3 can be equivalent to

![](img/5682e787fc967e93d7e33e8bac5f58a0_503_0.png)

```cpp
template <typename T, int Size>
class fsize_vector
{
    template <typename Vector>
    self& operator=(const Vector& that)
    {
        data[0]= that[0];
        data[1]= that[1];
        data[2]= that[2];
    }
};
```

The right-hand-side vector that might be an expression template (§5.3) for, say, alpha * x + y and its evaluation can be also inlined as well:

![](img/5682e787fc967e93d7e33e8bac5f58a0_503_1.png)

```cpp
template <typename T, int Size>
class fsize_vector
{
    template <typename Vector>
    self& operator=(const Vector& that)
    {
        data[0]= alpha * x[0] + y[0];
        data[1]= alpha * x[1] + y[1];
        data[2]= alpha * x[2] + y[2];
    }
};
```

To make the unrolling more explicit and for the sake of introducing meta-tuning step by step, we develop a (static) functor⁹ that performs the assignment:

9. Technically, it is not really a functor since it has no operator(). Since operators cannot be declared static, we use the function eval which we consider as a static equivalent of the
