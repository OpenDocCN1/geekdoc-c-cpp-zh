amount accumulated when the interest is compounded continuously. It also appears in problems relating to exponential growth and decay. It is known that $e$ is an irrational number. The value of $e$ to nine decimal places is $e = 2.718281827$. Write a program that computes the value of the expression $\lim_{n \to \infty} \left(1 + \frac{1}{n}\right)^n$ between certain values of $n$ and then compare the values with $e$. For example, you can compute the values of the expression between 100 and 10,000 with an increment of 100, or between 1,000 and 1,000,000 with an increment of 1,000.

+   31. Exercise 30 defines the number $e$. The value of $e$ can be approximated using the following expression:
+   
+   $$2 + \frac{1}{2!} + \frac{1}{3!} + \cdots + \frac{1}{n!},$$
+   
+   where $n$ is a positive integer. Write a program that uses this formula to approximate the value of $e$. Test your program for $n = 4, 8, 10,$ and $12$.
+   
+   32. Exercise 30 defines the number $e$ and Exercise 31 shows how to approximate the value of $e$ using a different expression. Interestingly, the value of $e$ can also be approximated using the following expression:
+   
+   $$2 + \frac{1}{1 + \frac{1}{2 + \frac{2}{3 + \frac{3}{4 + \frac{4}{5 + \frac{5}{\ddots + \frac{n-1}{(n-1) + \frac{n-1}{n+n}}}}}}}}}$$
+   
+   Write a program that uses this formula to approximate the value of $e$. Test your program for $n = 3, 5, 10, 50,$ and $100$.
+   
+   33. Bianca is preparing special dishes for her daughter's birthday. It takes her $a$ minutes to prepare the first dish, and each following dish takes $b$ minutes longer than the previous dish. She has $t$ minutes to prepare the dishes. For example, if the first dish takes $a = 10$ minutes and $b = 5$, then the second dish will take 15 minutes, the third dish will take 20 minutes, and so on. If she has 80 minutes to prepare the dishes, then she can prepare four dishes because $10 + 15 + 20 + 25 = 70$. Write a program that prompts the user to enter the values of $a$, $b$, and $t$, and outputs the number of dishes Bianca can prepare.