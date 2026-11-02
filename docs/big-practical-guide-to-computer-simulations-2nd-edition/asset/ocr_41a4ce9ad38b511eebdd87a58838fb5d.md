# (6) **Integration of function**

Write a function which integrates a one-dimensional function $f(x)$ over the interval $[x_1, x_2]$ via the trapezoidal rule, i.e. calculates

$$I = \sum_{t=0}^{t_{\max}-1} \frac{f(x_1 + t\Delta) + f(x_1 + (t+1)\Delta)}{2} \Delta$$ 
$$= \frac{f(x_1)}{2} \Delta + \sum_{t=1}^{t_{\max}-1} f(x_1 + t\Delta)\Delta + \frac{f(x_2)}{2} \Delta$$

where $t_{\max}$ is the number of integration steps and $\Delta = (x_2 - x_1)/t_{\max}$. The function prototype reads as follows:

| SOLUTION SOURCE CODE |
|---|
| DIR: c-programming<br>FILE(S):<br>integration.c |

```
```c
/******************** integrate() ***********************/
/** Integrates a 1-dim function numerically using **/
/** the trapezoidal rule **/
/** PARAMETERS: (*)= return-parameter **/
/**    from: startpoint of interval **/
/**      to: endpoint of interval **/
/** num_steps: number of integration steps **/
/**      f: p. to function to be integrated **/
/** RETURNS: **/
/**    value of integral **/
/*******************************************************/
double integrate(double from, double to, int num_steps,
                 double (* f)(double))
```
```

Test the function in your `main()` function by integrating the `sin()` function defined in `math.h` over different intervals, for example $[0, \pi/2]$, $[0, \pi]$.

# (7) **Optimizing code by compiler**

Get the program `optimization.c` which calculates for a set of numbers for all possible subsets of the numbers the sum. This takes exponentially long in the number of numbers, hence it is a good testbed to see the effect of compiler optimization.

| GET SOURCE CODE |
|---|
| DIR: c-programming<br>FILE(S):<br>optimization.c |

Compile the program via `cc -o optimization optimization.c -lm -Ox`, where x is 0, 1, 2, and 3. Measure the running time for executing the compiled program via `time optimization` (note that the program does not print anything in the standard version).