+   1. Write a program that calculates sin(x) as the finite sum (3.46). (If you already did this in Chapter 2, then you may reuse that program and its results here. But remember, you should not be using factorials in the algorithm.)
+   2. Calculate your series for x ≤ 1 and compare it to the built-in function Math.sin(x) (you may assume that the built-in function is exact). Stop your summation at an N value for which the next term in the series will be no more than 10⁻⁷ of the sum up to that point,
+   
+   $$\frac{|(-1)^N x^{2N+1}|}{(2N-1)!} \le 10^{-7} \left|\sum_{n=1}^{N} \frac{(-1)^{n-1} x^{2n-1}}{(2n-1)!}\right|.$$ (3.47)
+   3. Examine the terms in the series for x ≈ 3π and observe the significant subtractive cancelations that occur when large terms add together to give small answers. (Do not use the identity sin(x+2π)=sin x to reduce the value of x in the series.) In particular, print out the near-perfect cancelation around n ≈ x/2.
+   4. See if better precision is obtained by using trigonometric identities to keep 0 ≤ x ≤ π.
+   5. By progressively increasing x from 1 to 10, and then from 10 to 100, use your program to determine experimentally when the series starts to lose accuracy and when it no longer converges.
+   6. Make a series of graphs of the error vs. N for different values of x. You should get curves similar to those in Figure 3.4.

![](bbox=[0.22, 0.55, 0.76, 0.81])

Figure 3.4 The error in the summation of the series for e⁻ˣ vs. N for various x values. The values of x increase vertically for each curve. Note that a negative initial slope corresponds to decreasing error with N, and that the dip corresponds to a rapid convergence followed by a rapid increase in error. (Courtesy of J. Wiren.)