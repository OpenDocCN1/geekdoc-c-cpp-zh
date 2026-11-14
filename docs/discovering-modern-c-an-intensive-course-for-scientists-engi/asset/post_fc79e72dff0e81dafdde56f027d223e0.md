
- 4. Both types are completely known and we can statically down-cast this pointer to point*.
- 5. Since we know that the this pointer of inequality<point> is an up-casted this pointer to point it is safe to down-cast it to its original type.
- 6. The equality operator of point is called and instantiated (if not done before).

Every class U with an equality operator can be derived from inequality<U> in the same manner. A collection of such CRTP templates for operator defaults is provided by Boost.Operators from Jeremy Siek and David Abrahams.

### 6.6.2 A Reusable Access Operator

```
=> c++11/matrix_crtp_example.cpp
```

The CRTP idiom allows us to tackle a problem mentioned earlier (§2.6.4): accessing multi-dimensional data structures with the bracket operator with a reusable implementation. At the time we did not know the necessary language features, especially templates and inheritance. Now we do and will apply this knowledge to realize two bracket operator calls by one of a binary call operator, i.e., evaluate A[i][j] as A(i, j).

Say we have a matrix type going by the elegant name some_matrix whose operator() accesses only a_ij. For consistency with the vector notation, we prefer bracket operators. Those accept only one argument, and we therefore need a proxy that represents the access to a matrix row. This proxy provides in turn a bracket operator for accessing a column in the corresponding row, i.e., yields an element of the matrix:

```
class some_matrix; // Forward declaration

class simple_bracket_proxy
{
public:
    simple_bracket_proxy(some_matrix& A, size_t r) : A(A), r(r) {}

    double& operator[](size_t c){ return A(r, c); } // Error
private:
    some_matrix& A;
    size_t r;
};

class some_matrix
{
// ...

    double& operator()(size_t r, size_t c) { ... }

    simple_bracket_proxy operator[](size_t r)
    {
        return simple_bracket_proxy(*this, r);
    }
};
```

The idea is that A[i] returns a proxy p referring to A and containing i. Calling A[i][j] corresponds to p[j] which in turn should call A(i, j). Unfortunately, this code does not compile. When we call some_matrix::operator() in simple_bracket_proxy::operator[], the type some_matrix is only declared but not fully defined. Switching the two class definitions would only reverse the dependency and lead to more uncompilable code. The problem in this proxy implementation is that we need two complete types that depend on each other.

This is an interesting aspect of templates: they allow us to break mutual dependencies thanks to their postponed code generation. Adding template parameters to the proxy removes the dependency:

```cpp
template <typename Matrix, typename Result>
class bracket_proxy
{
public:
    bracket_proxy(Matrix& A, size_t r) : A(A), r(r) {}

    Result& operator[](size_t c){ return A(r, c); }

private:
    Matrix& A;
    size_t r;
};

class some_matrix
{
    // ...
    bracket_proxy<some_matrix, double> operator[](size_t r)
    {
        return bracket_proxy<some_matrix, double>(*this, r);
    }
};
```

Finally, we can write A[i][j] and have it performed internally in terms of the two-argument operator(). Now we can write many matrix classes with entirely different implementations of operator(), and all of them can deploy bracket_proxy in exactly the same manner.

Once we have implemented several matrix classes, we realize that the operator[] looks quite the same in all matrix classes: just returning a proxy with the matrix reference and the row argument. We can add another CRTP class for implementing this bracket operator just once:

```cpp
template <typename Matrix, typename Result>
class bracket_proxy { ... };

template <typename Matrix, typename Result>
class crtp_matrix
{
    using const_proxy = bracket_proxy<const Matrix, const Result>;

public:
    bracket_proxy<Matrix, Result> operator[](size_t r)
    {
        return {static_cast<Matrix&>(*this), r};
    }

    const_proxy operator[](size_t r) const
    {
        return {static_cast<const Matrix&>(*this), r};
    }
};
class matrix
: public crtp_matrix<matrix, double>
{
    // ...
};
```

Note that the C++11 features are just used for brevity; we can implement this code as well in C++03 with little more verbosity. This CRTP matrix class can provide the bracket operator for every matrix class with a two-argument application operator. In a full-fledged linear-algebra package, however, we need to pay attention to which matrices are mutable and whether references or values are returned. These distinctions can be safely handled with meta-programming techniques from Chapter 5.

Although the proxy approach creates an extra object, our benchmarks have shown that the usage of the bracket operator is as fast as that of the application operator. Apparently, sophisticated reference forwarding in modern compilers can eliminate the actual creation of proxies.

## 6.7 Exercises

### 6.7.1 Non-redundant Diamond Shape

Implement the diamond shape from Section 6.3.2 such that the name is only printed once. Distinguish in derived classes between all_info() and my_info() and call the two functions appropriately.

### 6.7.2 Inheritance Vector Class

Revise the vector example from Chapter 2. Introduce the base class vector_expression for size and operator(). Make vector inherit from this base class. Then make a class ones that is a vector of all ones and also inherits from vector_expression.

### 6.7.3 Clone Function

Write a CRTP class for a member function named clone() that copies the current object—like the Java function clone (http://en.wikipedia.org/wiki/Clone_%28Java_method%29). Consider that the return type of the function must be the one of the cloned object.

## Chapter 7
Scientific Projects

In the preceding chapters, we focused primarily on language features of C++ and how we can best apply them to relatively small study examples. This last chapter should give you some ideas for how to build up larger projects. The first section (§7.1) from the author's friend Mario Mulansky deals with the topic of interoperability between libraries. It will give you a look behind the curtain at odeint: a generic library that seamlessly inter-operates with several other libraries in a very tight fashion. Then we will provide some background on how executables are built from many program sources and library archives (§7.2.1) and how tools can support this process (§7.2.2). Finally, we discuss how program sources are appropriately distributed over multiple files (§7.2.3).

### 7.1 Implementation of ODE Solvers

Written by Mario Mulansky

In this section we will go through the major steps for designing a numerical library. The focus here is not to provide the most complete numerical functionality, but rather to arrive at a robust design that ensures maximal generality. As an example, we will consider the numerical algorithms for finding the solution of Ordinary Differential Equations (ODEs). In the spirit of Chapter 3, our aim is to make the implementation as versatile as possible by using generic programming. We start by briefly introducing the mathematical background of the algorithms followed by a simple, straightforward implementation. From this, we will be able to identify individual parts of the implementation and one by one make them exchangeable to arrive at a fully generic library. We are convinced that after studying this detailed example of a generic library design, the reader will be able to apply this technique to other numerical algorithms as well.

### 7.1.1 Ordinary Differential Equations

Ordinary differential equations are a fundamental mathematical tool to model physical, biological, chemical, or social processes and are one of the most important concepts in science and engineering. Except for a few simple cases, the solution of an ODE cannot be found with analytical methods, and we have to rely on numerical algorithms to obtain at least an approximate solution. In this chapter, we will develop a generic implementation of the Runge-Kutta-4 algorithm, a general-purpose ODE solver widely used due to its simplicity and robustness.
