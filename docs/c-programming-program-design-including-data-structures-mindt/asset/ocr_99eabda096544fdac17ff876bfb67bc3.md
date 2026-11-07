+   8. Write a recursive function that returns `true` if the digits of a positive integer are in increasing order; otherwise, the function returns `false`. Also, write a program to test your function.

+   9. Write a recursive function, `reverseDigits`, that takes an integer as a parameter and returns the number with the digits reversed. Also, write a program to test your function.

+   10. Write a recursive function, `sumDigits`, that takes an integer as a parameter and returns the sum of the digits of the integer. Also, write a program to test your function.

+   11. Write a recursive function, `power`, that takes as parameters two integers $x$ and $y$ such that $x$ is nonzero and returns $x^y$. You can use the following recursive definition to calculate $x^y$:
+   
+   $$
+   power(x,y)=
+   \begin{cases}
+   1 & \text{if } y=0\\
+   x & \text{if } y=1\\
+   x \times power(x,y-1) & \text{if } y>1
+   \end{cases}
+   $$
+   
+   If $y<0$,
+   
+   $$power(x,y)=\frac{1}{power(x,-y)}.$$
+   
+   Also, write a program to test your function.

+   12. **(Greatest Common Divisor)** Given two integers $x$ and $y$, the following recursive definition determines the greatest common divisor of $x$ and $y$, written `gcd(x,y)`:
+   
+   $$
+   gcd(x,y)=
+   \begin{cases}
+   x & \text{if } y=0\\
+   gcd(y,x\%y) & \text{if } y\ne0
+   \end{cases}
+   $$
+   
+   **Note:** In this definition, `%` is the mod operator.
+   
+   Write a recursive function, `gcd`, that takes as parameters two integers and returns the greatest common divisor of the numbers. Also, write a program to test your function.

+   13. **(Ackermann’s Function)** The Ackermann’s function is defined as follows:
+   
+   $$
+   A(m,n)=
+   \begin{cases}
+   n+1 & \text{if } m=0\\
+   A(m-1,1) & \text{if } n=0\\
+   A(m-1,A(m,n-1)) & \text{otherwise}
+   \end{cases}
+   $$
+   
+   in which $m$ and $n$ are nonnegative integers. Write a recursive function to implement Ackermann’s function. Also write a program to test your function. What happens when you call the function with $m=4$ and $n=3$?