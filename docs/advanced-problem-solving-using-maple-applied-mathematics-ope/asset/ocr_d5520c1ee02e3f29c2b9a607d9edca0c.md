Section search is a type of bracketing method that uses the golden ratio. This recent technique was developed in 1953 by Jack Keifer.

To better understand the golden ratio, consider a line segment that is divided into two parts as shown in Figure 3.4. If the ratio of the length of the

![](bbox=[0.33, 0.19, 0.67, 0.244])

**FIGURE 3.4:** The Golden Ratio

the whole line to the length of the larger part is the same as the ratio of the length of the larger part to the length of the smaller part, we say the line is divided into the *golden ratio*. Symbolically, taking the length of the original segment as 1, this can be written as

$$\frac{1}{r} = \frac{r}{1-r}$$

Algebraic manipulation of the relationship above yields $r^2+r-1=0$. The quadratic’s positive root $r=(\sqrt{5}-1)/2$ satisfies the requirements for the line segment above. The golden ratio’s numerical value is $\phi\approx0.6180339880$. (The traditional symbol for the golden ratio is $\phi$.) The well-known ratio is the limiting value for the ratio of the consecutive terms of the Fibonacci sequences, which we will see in the next method. Another bracketing method, the *Fibonacci search* is often used in lieu of the Golden Section method.

In order to use the Golden Section search procedure, we must ensure that certain assumptions hold. These key assumptions are:

+   1. The function must be unimodal over a specified interval.
+   
+   2. the function must have an optimal solution over a known interval of uncertainty, and
+   
+   3. we will accept an interval solution since the exact optimal value cannot be found by bracketing, only approximated.

Only an *interval solution*, that is, an interval containing the exact optimal value, known as the *final interval of uncertainty*, can be found using this technique. The length of the final interval is controlled by the user and can be made arbitrarily small by selecting a *tolerance* value. Assuming unimodality guarantees that the final interval’s length is less than the chosen tolerance.

[^1]: See http://mathworld.wolfram.com/GoldenRatio.html.