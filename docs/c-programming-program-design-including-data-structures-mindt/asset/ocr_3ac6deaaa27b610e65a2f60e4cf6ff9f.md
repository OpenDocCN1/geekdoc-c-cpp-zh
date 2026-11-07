Write a program that prompts the user to enter the following:

+   a. The width of the river
+   b. The distance of the factory downstream on the other side of the river
+   c. The cost of laying the power line under water
+   d. The cost of laying the power line over land

The program then outputs the length of the power line that should run under water and the length that should run over land so the cost of constructing the power line is at the minimum. The program should also output the total cost of constructing the power line.

31. **(Pipe problem, requires trigonometry)** A pipe is to be carried around the right-angled corner of two intersecting corridors. Suppose that the widths of the two intersecting corridors are 5 feet and 8 feet (see Figure 6-19). Your objective is to find the length of the longest pipe, rounded to the nearest foot, that can be carried level around the right-angled corner.

![](bbox=[0.181, 0.461, 0.91, 0.588])

**FIGURE 6-19**  Pipe problem

Write a program that prompts the user to input the widths of both of the hallways. The program then outputs the length of the longest pipe, rounded to the nearest foot, that can be carried level around the right-angled corner. (Note that the length of the pipe is given by \(l = AB + BC = 8/\sin(\theta) + 5/\cos(\theta)\), where \(0 < \theta < \pi/2\).)

32. Let **a** and **b** be integers such that either **a** or **b** is nonzero. The greatest common divisor, written \(gcd(a,b)\), of **a** and **b** is the largest positive integer that divides both **a** and **b**. Your program must contain a function that takes as input two integers and returns the \(gcd\) of the integers.

33. Example 6-16 shows how to write a program to factor a polynomial of the form \(ax^2 + bx + c\), where **a**, **b**, and **c** are integers. Modify the program so that it can also factor polynomials of the form \(ax^2 + bx + c\), where **a**, **b**, and **c** are integers. Note that the polynomial \(-2x^2 - 3x + 2\) can be factored as: \(-2x^2 - 3x + 2 = (-2x + 1)(x + 2) = -(2x - 1)(x + 2)\).