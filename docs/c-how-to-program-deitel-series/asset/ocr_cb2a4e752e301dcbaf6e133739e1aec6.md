```
```cpp
cout << " ";
cout << '*';
cout << endl;
```
```

```
```text
* * * * * * * *
 * * * * * * * *
* * * * * * * *
 * * * * * * * *
* * * * * * * *
 * * * * * * * *
* * * * * * * *
 * * * * * * * *
* * * * * * * *
```
```

**4.29**   *(Multiples of 2 with an Infinite Loop)* Write a program that prints the powers of the integer 2, namely 2, 4, 8, 16, 32, 64, etc. Your while loop should not terminate (i.e., you should create an infinite loop). To do this, simply use the keyword `true` as the expression for the while statement. What happens when you run this program?

**4.30**   *(Calculating a Circle's Diameter, Circumference and Area)* Write a program that reads the radius of a circle (as a double value) and computes and prints the diameter, the circumference and the area. Use the value 3.14159 for π.

**4.31**   What’s wrong with the following statement? Provide the correct statement to accomplish what the programmer was probably trying to do.

```cpp
cout << ++(x + y);
```

**4.32**   *(Sides of a Triangle)* Write a program that reads three nonzero double values and determines and prints whether they could represent the sides of a triangle.

**4.33**   *(Sides of a Right Triangle)* Write a program that reads three nonzero integers and determines and prints whether they’re the sides of a right triangle.

**4.34**   *(Factorial)* The factorial of a nonnegative integer *n* is written *n*! (pronounced “n factorial”) and is defined as follows:

$$n! = n \cdot (n - 1) \cdot (n - 2) \cdot \ldots \cdot 1 \quad \text{(for values of } n \text{ greater than 1)}$$

and

$$n! = 1 \quad \text{(for } n = 0 \text{ or } n = 1\text{).}$$

For example, $5! = 5 \cdot 4 \cdot 3 \cdot 2 \cdot 1$, which is 120. Use while statements in each of the following:

+   a) Write a program that reads a nonnegative integer and computes and prints its factorial.

+   b) Write a program that estimates the value of the mathematical constant $e$ by using the formula:
+   
+   $$e = 1 + \frac{1}{1!} + \frac{1}{2!} + \frac{1}{3!} + \ldots$$
+   
+   Prompt the user for the desired accuracy of $e$ (i.e., the number of terms in the summation).

+   c) Write a program that computes the value of $e^x$ by using the formula
+   
+   $$e^x = 1 + \frac{x}{1!} + \frac{x^2}{2!} + \frac{x^3}{3!} + \ldots$$
+   
+   Prompt the user for the desired accuracy of $e$ (i.e., the number of terms in the summation).

**4.35**   *(C++11 List Initializers)* Write statements that use C++11 list initialization to perform each of the following tasks:

+   a) Initialize the unsigned int variable `studentCounter` to 0.
+   
+   b) Initialize the double variable `balance` to 1000.0.