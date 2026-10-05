# Chapter 2 ■ Numerical Algorithms 51

Figure 2-8 shows the NewtonsMethod sample program, which is available for download on this book's website. This program uses Newton's method three times to find the three roots of the function y = x^3 / 5 - x^2 + x. Circles show the program's guesses as it searches for each root.

![](bbox=[0.19, 0.183, 0.659, 0.497])

Figure 2-8: The NewtonsMethod sample program demonstrates Newton's method to find the three roots of the function y = x^3 / 5 - x^2 + x.

# Summary

Some numerical algorithms, such as randomization, are useful in a wide variety of applications. Other algorithms, such as prime factoring and finding the greatest common divisor, have much limited use. If your program doesn't need to find greatest common divisors, the GCD algorithm won't be much help.

However, the techniques and concepts demonstrated by these algorithms can be useful in many other situations. For example, the idea that an algorithm can be probabilistic is very important in many applications. That idea can help you devise other algorithms that don't work with perfect certainty (and could easily be the subject of an interview question).

This chapter explained the ideas of fairness and bias, two very important concepts for any sort of randomized algorithm, such as the Monte Carlo integration algorithm, which was also described in this chapter.