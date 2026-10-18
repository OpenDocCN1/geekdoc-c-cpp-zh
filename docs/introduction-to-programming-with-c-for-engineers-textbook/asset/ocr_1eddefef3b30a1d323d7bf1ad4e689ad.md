where $\delta$ is a parameter. For sufficiently low values of $\delta$, the previous equation can be approximated as follows (Press et al. 2007):

$f'(x) \approx \frac{f(x+\varepsilon)-f(x)}{\varepsilon}$  (3.5)

The previous formula gives us a practical method for computing $f'$, given $f$ and $x$ and choosing $\varepsilon$. In practice, the latter is set as a small value, but large enough compared to the computer’s precision to avoid excessive rounding errors (Section 7.4).

The `deriv` function follows Eq. (3.5):

```
```cpp
double deriv( double ( * f ) ( double ), double x, double eps = 1e-5 )
{
  // Let us use the definition of a derivative
  return ( f( x + eps ) - f( x ) ) / eps;
}
```
```

To allow computations for any function, a function pointer of type `double (*)(double)` is supplied on line [1] as the first argument of `deriv`. The next two arguments are a point $x$, at which we compute the derivative, and (obviously) the parameter `eps`. All of the computations take place on line [4], where a function, supplied by a pointer `f`, is called as if it were an ordinary function name.

Now we are able to compute real values. Let’s choose an interesting function $f(x)=x^x$, which can be easily coded as the following `pow_x_2_x`:

```
```cpp
double pow_x_2_x( double x )
{
  return pow( x, x );
}
```
```

We can compute the derivative of the previous function at a given point value. The necessary computations are performed in the following `deriv_test_fun` function:

```
```cpp
void deriv_test_fun( void )
{
  double x = 1.3;
  cout << "x2x'(x=1.3)" << deriv( pow_x_2_x, x ) << endl;
}
```
```

An interesting thing happens on line [13]: the `deriv` function takes as its first argument a function pointer that is simply the name of a function – `pow_x_2_x`, in this case. This works only under the condition that the formal and return parameters of the function and the function pointer agree. Hence it is important to remember that:

+   - The function name itself is a pointer to that function (i.e. its code)

This sometimes leads to unexpected errors. For example, the following code

```
```cpp
deriv_test_fun;
```
```