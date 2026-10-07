# Unsteady, Non-Linear, and Chaotic Systems

with decreasing error (4.533b) [(4.534b)]. The effects of step size h and order of approximation n on the order of the approximate (4.533a, b; 4.534a, b) versus the exact (4.531a–c) solution are considered next (note 4.12).

# NOTE 4.12: Effects of Step Size and Order of Approximation

The circular cosine has period $2\pi$ in (4.535a), and is skew-symmetric (symmetric) in the whole (4.535b) [half 4.535c]) interval:

```
$cos(x+2\pi)=\cos x, \cos(x+\pi)=-\cos x, \cos\left(\frac{\pi}{2}-x\right)=-\cos\left(\frac{\pi}{2}+x\right),$\n(4.535a–c)$
```

and thus it is sufficient to calculate it in one-quarter of the interval (4.536c) with equal steps:

```
$n=0,...,N=50: 0\le x\le\frac{\pi}{2}, x_n=nh, h=\frac{\pi}{2N}=\frac{\pi}{10}-\frac{\pi}{20}=0.3146,0.15708.\n(4.536–f)$
```

In (problem 159) Table 4.7 (4) are used 5 (10) steps (4.536a) [[4.536b]] of length (4.536e) [[4.536f]]) corresponding to angles $\theta=18^\circ$ ($9^\circ$). Table 4.7 compares at five points the exact solution (4.523d) with the approximate solution (4.530), using the first (second) order (4.533a) [[4.534a]] and the corresponding error (4.533b) [[4.534b]]. The lower (higher) approximation (4.533a) [[4.534a]]) applies only for $n\ge2($n\ge4$)$. The error increases with distance from the initial point, and the approximate solutions

# TABLE 4.7
Comparison of Exact and Approximate Solutions

| $n$ | $\theta$ | $x_n=n\pi/10$ | $\cos(x_n)$ | $y_n^{(1)}$ | $e_n^{(1)}$ | $y_n^{(2)}$ | $e_n^{(2)}$ |
|---|---|---|---|---|---|---||}{
| 0 | $0^\circ$ | 0.000 | 1.000 | 1.000 | 0.000 | 1.000 | 0.000 |
| 1 | $18^\circ$ | 0.314 | 0.951 | 1.000 | +0.0484 | 1.000 | +0.0484 |
| 2 | $36^\circ$ | 0.628 | 0.809 | 0.901 | +0.0929 | 0.910 | +0.0929 |
| 3 | $54^\circ$ | 0.942 | 0.587 | 0.703 | +0.1116 | 0.731 | +0.1163 |
| 4 | $72^\circ$ | 1.256 | 0.309 | 0.407 | +0.0981 | 0.417 | +0.1085 |
| 5 | $90^\circ$ | 1.570 | 0.000 | 0.013 | +0.0143 | 0.064 | +0.0671 |

Note: The numerical solution of a differential equation leads to errors that: (i) increase with distance from the initial point; (ii) for the same distance from the initial point decrease for higher orders of the step size, e.g., $O(h^2)$ are more generally but not always more accurate $O(h)$ methods.