# 24.10 Integral on the Unit Interval

The above function is now used to integrate a polynomial of one variable over the unit interval [0,1], using the formula

$$\int_{0}^{1} p(x)dx = P(1) - P(0) = P(1),$$

where P is the indefinite integral defined in the previous section:

```
template<class T>
const T
integral(const polynomial<T>&p) {
  return indefiniteIntegral(p)(1.);
} // integral on the unit interval
```

Indeed, after "indefiniteIntegral" is called to compute P, "operator()" is invoked to calculate the required number P(1).

# 24.11 Integral on the Unit Triangle

Consider now a polynomial of two variables p(x,y). Assume that x is a fixed number, so p(x,·) is actually a polynomial of one variable only. Let P be the indefinite integral of this polynomial (Section 24.9). Thus, P ≡ P(x,y), where x is a fixed parameter, and y is the only variable.

Let us now use P to calculate the integral of p over the unit triangle in Figure 5.5:

$$\int_{0}^{1}\int_{0}^{1-x} p(x,y)dy dx = \int_{0}^{1} P(x,1-x)dx.$$

This formula is indeed implemented below:

```
template<class T>
const T
integral(const polynomial<polynomial<T> >&p) {
```

First, we use the constructor that takes two "double" arguments to form the polynomial 1−x: This polynomial is then stored in a local polynomial object named "oneMinusx":

```
polynomial<T> oneMinusx(1., -1.);
```

Next, the "indefiniteIntegral" function is applied to the original polynomial `p` to form the indefinite integral with respect to y (denoted by P in the above formula). Then, "operator()" of Section 24.6 is applied to P(x,y) (with the polynomial argument 1−x) to substitute 1−x for y and produce P(x,1−x). Indeed, the argument of "operator()" can be not only a mere scalar but also a polynomial of one variable, so the template class `S` in Section 24.6 is interpreted as a polynomial of one variable as well. Finally, the original version of "integral()" is applied to P(x,1−x) to integrate over the unit interval:

```
return
  integral(indefiniteIntegral(p)(oneMinusx));
} // integral on the unit triangle
```