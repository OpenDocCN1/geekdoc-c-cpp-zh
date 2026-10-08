+   13. Why would you format your input rather than just having the file contain “the numbers”?

+   14. How do you plan the general layout of a graph? How do you reflect that layout in your code?

# Terms

+   - approximation
- default argument
- function
- lambda
- scaling
- screen layout

# Exercises

+   1. Here is another way of defining a factorial function:

   ```c
   int fac(int n) { return n>1 ? n*fac(n-1) : 1; } // factorial n!
   ```

   It will do **fac(4)** by first deciding that since **4>1** it must be **4\*fac(3)**, and that’s obviously **4\*3\*fac(2)**, which again is **4\*3\*2\*fac(1)**, which is **4\*3\*2\*1**. Try to see that it works. A function that calls itself is said to be *recursive*. The alternative implementation in §15.5 is called *iterative* because it iterates through the values (using **while**). Verify that the recursive **fac()** works and gives the same results as the iterative **fac()** by calculating the factorial of $0, 1, 2, 3, 4$, up until and including 20. Which implementation of **fac()** do you prefer, and why?

+   2. Define a class **Fct** that is just like **Function** except that it stores its constructor arguments. Provide **Fct** with “reset” operations, so that you can use it repeatedly for different ranges, different functions, etc.

+   3. Modify **Fct** from the previous exercise to take an extra argument to control precision or whatever. Make the type of that argument a template parameter for extra flexibility.

+   4. Graph a sine (**sin()**), a cosine (**cos()**), the sum of those (**sin(x)+cos(x)**), and the sum of the squares of those (**sin(x)\*sin(x)+cos(x)\*cos(x)**) on a single graph. Do provide axes and labels.

+   5. “Animate” (as in §15.5) the series **1−1/3+1/5−1/7+1/9−1/11+ …**. It is known as Leibniz’s series and converges to pi/4.

+   6. Design and implement a bar graph class. Its basic data is a **vector<double>** holding $\mathcal{N}$ values, and each value should be represented by a “bar” that is a rectangle where the height represents the value.

+   7. Elaborate the bar graph class to allow labeling of the graph itself and its individual bars. Allow the use of color.

+   8. Here is a collection of heights in centimeters together with the number of people in a group of that height (rounded to the nearest 5cm): (170,7), (175,9), (180,23), (185,17), (190,6), (195,1). How would you graph that