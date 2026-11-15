![](bbox=[0.24, 0.08, 0.91, 0.53])

Figure 6.4 Program output for four intervals.

Figure 6.4 contains plots of the 21 values computed for four different intervals [a, b]. The program computes only 21 values, so the resolution in the plots is affected by the size of the interval: A smaller interval has better resolution than a larger interval. Note that the main function of solution 2 is easier to read because it is shorter than the main function in the first solution.

The main function in solution 2, and the main function in program chapter6_1 each contained a function prototype statement that was placed above the main function. In the following section we discuss function prototypes and look more closely at the interaction between a statement that references a function and the function definition itself.

# Function Prototype

The solution presented in program chapter6_3 contained the following statement above the main function definition:

```
double sinc(double x );
```

This statement is called a function prototype. The prototype declares that sinc( ) expects an argument of type double and returns a value of type double. The compiler can now