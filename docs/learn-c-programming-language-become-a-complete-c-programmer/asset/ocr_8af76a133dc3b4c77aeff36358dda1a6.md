It is important that this refinement of the implementation of **Vector** be achieved without affecting the interface presented to users. Specialization is a way of specifying alternative implementations for different uses of a common interface. Naturally, we could have given the general **Vector** and the **Vector** of pointers different names. However, when I tried that, many people who should have known better forgot to use the pointer classes and found their code much larger than expected. In this case, it is much better to hide the crucial implementation details behind a common interface.

This technique proved successful in curbing code bloat in real use. People who do not use a technique like this (in C++ or in other languages with similar facilities for type parameterization) have found that replicated code can cost megabytes of code space even in moderately sized programs. By eliminating the time needed to compile those additional versions of the **Vector** operations, this technique can also cut compile and link times dramatically. Using a single specialization to implement all lists of pointers is an example of the general technique of minimizing code bloat by maximizing the amount of shared code.

Some compilers are getting smart enough to perform this particular optimization without help from the programmer, but the technique is generally applicable and useful. Variants of the technique of using a single run-time representation for values of a number of types and relying on the (static) type system to ensure that they are used only according to their declared type has been called *type erasure*. In the context of C++, it was first documented in the original template paper [Stroustrup,1988].

# 25.3.1 Interface Specialization

Sometimes, a specialization is not an algorithmic optimization, but a modification of an interface (or even a representation). For example, the standard library **complex** uses specializations to adjust the set of constructors and the argument types for important operations for important specializations (such as **complex<float>** and **complex<double>**). The general (primary) template (§25.3.1.1) looks like this:

```
template<typename T>
class complex {
public:
complex(const T& re = T{}, const T& im = T{});
complex(const complex&); // copyconstructor
template<typename X>
complex(const complex<X>&); // conversion from complex<X> to complex<T>
complex& operator=(const complex&);
complex<T>& operator=(const T&);
complex<T>& operator+=(const T&);
//...
template<typename X>
complex<T>& operator=(const complex<X>&);
template<typename X>
```