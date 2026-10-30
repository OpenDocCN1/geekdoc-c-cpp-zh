+   3. Apply the modified Newton’s method to find the following:
+      a. Maximize \(f(x,y)=-x^3+3x+84y-6y^2\) starting with the initial value \(\langle1,1\rangle\). Why can’t we start at \(\langle0,0\rangle\)?
+      b. Minimize \(f(x,y)=-4x+4x^2-3y+y^2\) starting at \(\langle0,0\rangle\).
+      c. Perform 3 modified Newton’s method iterations to minimize \(f(x,y)=(x-2)^4+(x-2y)^2\) starting at \(\langle0,0\rangle\). Why is this problem not converging as quickly as b?

4. Use a gradient search to approximate the minimum to \(f(x)=(x_1-2)^2+x_1+x_2^2\). Start at \(\langle2.5,1.5\rangle\).

# Projects

**Project 4.1.** Modify the Steepest Ascent Algorithm (pg 147) to approximate the minimum of a function. This technique is called the *Steepest Descent Algorithm*.

**Project 4.2.** Write a program in Maple that uses the one-dimensional Golden Section search algorithm instead of calculus to perform iterations of a gradient search. Use your code to find the maximum of

\[
f(x,y)=xy-x^2-y^2-2x-2y+4
\]

**Project 4.3.** Write a program in Maple that uses the one-dimensional Fibonacci search algorithm instead of calculus to perform iterations of a gradient search. Use your code to find the maximum of

\[
f(x,y)=xy-x^2-y^2-2x-2y+4
\]

# References and Further Reading

[B2016] William C. Bauldry, *Introduction to Computation*, 2016.

[BSS2013] Mokhtar S. Bazaara, Hanif D. Sherali, and Chitharanjan M. Shetty, *Nonlinear Programming: Theory and Algorithms*, Wiley, 2013.

[F1992] William P. Fox, “Teaching nonlinear programming with Minitab,” *COED Journal*, Vol. II (1992), no. 1, 80–84.