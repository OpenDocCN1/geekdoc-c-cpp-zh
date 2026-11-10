3. We substitute the Taylor polynomial in Gauss formula:

```
~~~sage
sage: x = var('x'); f(x) = taylor(arctan(x), x, 0, 21)
sage: approx = 4 * (12 * f(1/38) + 20 * f(1/57)
....:          + 7 * f(1/239) + 24 * f(1/268))
sage: approx.n(digits = 50); pi.n(digits = 50)
3.1415926535897932384626433832795028841971693993751
3.1415926535897932384626433832795028841971693993751
sage: approx.n(digits = 50) - pi.n(digits = 50)
9.644474859113248678542091753740470529297881708080e-37
~~~
```

**Exercise 5 page 32.** *(Asymptotic expansion of a sequence)* One can easily show that \(x_n \sim n\pi\), that is \(x_n = n\pi + o(n)\).

We inject this equality into the following equation, which we obtain from \(\arctan x + \arctan(1/x) = \pi/2\):

$$x_n = n\pi + \frac{\pi}{2} - \arctan\left(\frac{1}{x_n}\right)$$

We then inject the asymptotic expansions of \(x_n\) obtained in this equation, and so on (method of successive refinements).

As we know that at each step, an order-\(p\) expansion allows to get an order-\((p+2)\) expansion, we obtain, in four steps, an expansion at order 6. Anticipating on Chapter 3, we can program these four steps into a loop:

```
~~~sage
sage: n = var('n'); phi = lambda x: n*pi + pi/2 - arctan(1/x)
sage: x = n*pi
sage: for i in range(4):
....:     x = taylor(phi(x), n, infinity, 2*i); x
~~~
```

Finally, we obtain:

$$x_n = \frac{1}{2}\pi + \pi n - \frac{1}{\pi n} + \frac{1}{2}\frac{1}{\pi^2 n^2} - \frac{1}{12}\frac{3\pi^2+8}{\pi^3 n^3} - \frac{1}{8}\frac{1}{\pi^2 n^4} - \frac{1}{240}\frac{15\pi^4+240\pi^2+208}{\pi^5 n^5} + \frac{1}{96}\frac{3\pi^4+80\pi^2+208}{\pi^6 n^6} + O\left(\frac{1}{n^7}\right).$$

**Exercise 6 page 33.** *(A counter-example to Schwarz theorem due to Peano)* The partial applications \(f(x,0)\) and \(f(0,x)\) are identically zero in \((0,0)\); without any computation we deduce that \(\partial_1 f(0,0)=\partial_2 f(0,0)=0\). Then we compute the second order partial derivative in \((0,0)\):

```
~~~sage
sage: h = var('h'); f(x, y) = x * y * (x^2 - y^2) / (x^2 + y^2)
sage: D1f(x, y) = diff(f(x,y), x); limit((D1f(0,h) - 0) / h, h=0)
-1
sage: D2f(x, y) = diff(f(x,y), y); limit((D2f(h,0) - 0) / h, h=0)
1
sage: g = plot3d(f(x, y), (x, -3, 3), (y, -3, 3))
~~~
```