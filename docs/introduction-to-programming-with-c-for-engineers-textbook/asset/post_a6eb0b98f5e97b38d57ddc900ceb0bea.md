
## 7.4.8 Example Project – The Newton Method of Finding the Roots of a Function

Many tasks require finding the roots of a function: the arguments for which a function equals zero, as shown in Figure 7.14. For example, in optimization problems, finding the roots of the derivative of a function lets us find local extreme values of that function. We will use this feature to derive an algorithm for computing the roots of a function.

![img/31dee73f41f3d43a1f2e2b4eaffa2afd_555_0.png]

**Figure 7.14** Plot of a function having two roots: i.e. it crosses the abscissa at two points x₀₁ and x₀₂.

More formally, for a function *f(x)*, we are looking for values *x* that fulfill the following condition:

$$f(x)=0$$

Once again, to implement a software component composed of a number of using declarations and functions, we will use the encompassing namespace rather than a class. In our example, the namespace NewtonZero starts line [8]. At first, it is convenient to introduce some type aliases with the using directive. On line [10], the FP alias is defined to represent floating-point values throughout the namespace. Such a grouping allows for flexible changes if, for instance, we wished to verify operations with float. Line [11] introduces the alias to represent real-valued functions, as discussed in Section 3.14.9. In that section, we also discussed the deriv function; for convenience, it is repeated here, starting on line [14].

```
// Derivative is also a 1D real function
auto deriv( const Real_Fun & fun, const FP x0, const FP eps = 1e-5 )
{
```

The function FindZero on line [34] iteratively computes a root of its supplied function fun. The computations follow Algorithm 7.1 and the scheme outlined in Listing 7.13. Hence, on line [38], the machine epsilon value is read, which is then used to set the threshold as discussed in Section 7.4.2. The iterating loop starts on line [46]. At each step, on line [51], a function derivative is computed at point x_n by calling deriv. But since we will divide by this value, line [54] checks whether it is sufficiently large. Otherwise, the loop is terminated. Here we simply use the epsilon in the role of the minimal threshold of the divisor (see question no. 26 in Q&E).

```
// Finds zero crossing of the supplied function
//
// INPUT: fun - a function object
// start_x - estimated starting point
// thresh - a convergence threshold
// OUTPUT:
// // a tuple containing a pair of values:
// // - the found zero position
// // - true if computations converged
// // REMARKS:
// // Only if true is returned can the result be valid
auto FindZero( const Real_Fun & fun, const FP start_x, const FP thresh = 1e-10 )
{
```

```
FP x_n { start_x };
```

The parameter `delta` is computed on line [58], exactly as stated in Eq. (7.48). The convergence condition is checked on line [61]. For this purpose, `delta` is directly checked, since it is the difference between consecutive values of the variable `x_n` (compare this with line [97] in Listing 7.13). If the computations converged, i.e. the modulus of `delta` is less than the local threshold computed on line [49], then the loop terminates. This is also the only case when the parameter `reach_converg` is set to true. It is used to distinguish loop termination resulting from other reasons, in which case we cannot provide a valid result. However, if there is no convergence at this step, `x_n` is updated on line [67] exactly as in step 4 of Algorithm 7.1. On line [71], `FindZero` returns a pair: the last value of `x_n` and the flag `reach_converg`. The former constitutes a valid result only if the latter is set to true. This pair is represented by the `std::tuple` object, created by the `std::make_tuple` helper function. This is an efficient method for a function to return many values at once, as discussed in Section 3.17.1. Otherwise, if `reach_converg` is false, then the loop terminates by exceeding the number of allowable iterations set in `kMaxIters`. This also means a lack of convergence.

The operation of the `FindZero` function is verified to solve the equation $x^2+x-6=0$, starting at point $-1.5$, as set on line [6] of the function `NewtonZero_Test` in the following code. Although the first parameter is an object defined with `std::function`, a lambda function (Section 3.14.6) can also be provided, as shown on line [6].

```
namespace NewtonZero
{

    void NewtonZero_Test( void )
    {
        auto [ val,flag ] = FindZero( [] ( double x ) { return x*x+x-6.0; }, -1.5 );

        std::cout<<"Zero at "<<( flag ? std::to_string(val) : "none" ) << std::endl;
    }
}
```

On line [8], `std::to_string` is called, which converts `val` to `std::string`. This is required in this context, since the `? :` operator expects the same types on both sides of its colon `:`.

It is easy to verify that this square equation has two solutions $x_1=-3.0$ and $x_2=2.0$. Which one is reached depends on the starting point provided as the second parameter to `FindZero`. Hence, the analytical solution has its own advantages, as shown in Section 3.16. But the advantage of the numerical approach, as presented in the `FindZero` function, is that it can work with any provided function. Nevertheless, it requires an initial starting value and threshold, and it operates in an iterative fashion.

# 7.4.8.1  Function to Compute Square Roots Based on Newton’s Iteration

As alluded to previously, finding the roots of a function has many applications, such as optimization problems. Another interesting application is computing functions for which there is no simple implementation. In computations, another function is used, for which we have an easy algorithm. To demonstrate this method, we will compute the square root for a given real value. To see how we can use Newton’s method to compute a square root, let’s start with the function we wish to compute:

$$f(x)=\sqrt{x} \tag{7.49}$$

It can be written as follows:

$$y=\sqrt{x}$$

Naturally, we assume we do not know how to directly compute $\sqrt{x}$. However, if we square both sides of the previous equation, we get the following

$$y^2=x$$

which after rearranging yields

$$y^2-x=0$$
