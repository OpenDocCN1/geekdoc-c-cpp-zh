```
namespace std {
    // types
    using fenv_t      = object type;
    using fexcept_t = integer type;

    // functions
    int feclearexcept(int except);
    int fegetexceptflag(fexcept_t* pflag, int except);
    int feraiseexcept(int except);
    int fesetexceptflag(const fexcept_t* pflag, int except);
    int fetestexcept(int except);

    int fegetround();
    int fesetround(int mode);

    int fegetenv(fenv_t* penv);
    int feholdexcept(fenv_t* penv);
    int fesetenv(const fenv_t* penv);
    int feupdateenv(const fenv_t* penv);
}
```

1 The contents and meaning of the header <cfenv> are the same as the C standard library header <fenv.h>.

> [Note 1: This document does not require an implementation to support the FENV_ACCESS pragma; it is implementation-defined (15.9) whether the pragma is supported. As a consequence, it is implementation-defined whether these functions can be used to test floating-point status flags, set floating-point control modes, or run under non-default mode settings. If the pragma is used to enable control over the floating-point environment, this document does not specify the effect on floating-point evaluation in constant expressions. — end note]

SEE ALSO: ISO C 7.6

# 26.3.2 Threads [cfenv.thread]

1 The floating-point environment has thread storage duration (6.7.5.3). The initial state for a thread’s floating-point environment is the state of the floating-point environment of the thread that constructs the corresponding thread object (32.4.3) or jthread object (32.4.4) at the time it constructed the object.

> [Note 1: That is, the child thread gets the floating-point state of the parent thread at the time of the child’s creation. — end note]

2 A separate floating-point environment is maintained for each thread. Each function accesses the environment corresponding to its calling thread.

# 26.4 Complex numbers [complex.numbers]

# 26.4.1 General [complex.numbers.general]

1 The header <complex> defines a class template, and numerous functions for representing and manipulating complex numbers.

2 The effect of instantiating the template complex for any type other than float, double, or long double is unspecified. The specializations complex<float>, complex<double>, and complex<long double> are literal types (6.8).

3 If the result of a function is not mathematically defined or not in the range of representable values for its type, the behavior is undefined.

4 If z is an lvalue of type cv complex<T> then:

+   (4.1) — the expression reinterpret_cast<cv T(&)[2]>(z) is well-formed,
+   (4.2) — reinterpret_cast<cv T(&)[2]>(z)[0] designates the real part of z, and
+   (4.3) — reinterpret_cast<cv T(&)[2]>(z)[1] designates the imaginary part of z.

Moreover, if a is an expression of type cv complex<T>* and the expression a[i] is well-defined for an integer expression i, then:

+   (4.4) — reinterpret_cast<cv T*>(a)[2*i] designates the real part of a[i], and
+   (4.5) — reinterpret_cast<cv T*>(a)[2*i + 1] designates the imaginary part of a[i].