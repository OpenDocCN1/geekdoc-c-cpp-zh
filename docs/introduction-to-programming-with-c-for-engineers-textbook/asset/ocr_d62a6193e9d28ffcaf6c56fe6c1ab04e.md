![](bbox=[0.226, 0.099, 0.788, 0.158])

![](bbox=[0.225, 0.168, 0.788, 0.226])

![](bbox=[0.225, 0.239, 0.788, 0.296])

![](bbox=[0.225, 0.308, 0.789, 0.367])

**Figure 7.7** Distribution of positive floating-point values for *B* = 2, example precision *p*, and exponents *E*. Floating-point values are shown in red. It is easy to see different groups of number “concentrations” corresponding to different exponents *E*. For example, in plots (a) and (b), four groups are clearly visible, which correspond to *E* = -1, 0, 1, and 2. Spacing within the groups is the same. However, the spacing between the groups increases by a factor of the base *B*.

![](bbox=[0.226, 0.477, 0.789, 0.536])

**Figure 7.8** Distribution of positive floating-point values for *B* = 10, precision *p* = 2, and exponents *E*∈[-1,+1]. Floating-point values are shown in red.

+   - *Overflow* – The result is too large to be correctly represented
+   - *Underflow* – The result is too small to be correctly represented
+   - *Inexact* – The result cannot be represented exactly, so a rounded value is used instead
+   - *Invalid operation* – E.g. dividing by 0 or computing square root from a negative value

Investigating only the significand in Eq. (7.22), notice that the smallest possible positive value in the last position is simply for *a*<sub>p−1</sub> = 1, which can be expressed as follows:

$$\varepsilon = 1 \cdot B^{-(p-1)} = B^{1-p}. \tag{7.23}$$

The constant ε, called a *machine epsilon*, is one of the most important values characterizing computations with FP numbers. Since FP numbers are written in a normalized representation, as will be further discussed, ε can be interpreted as the distance between 1 and the closest value greater than 1 (not 0). We will see soon how ε can be used in practical computations with FP values.

For a given FP representation, such as float or double, the value of the machine epsilon can be easily computed, such as shown in Listing 7.12.