![](bbox=[0.24, 0.13, 0.72, 0.45])

FIGURE 13.19 Finite-difference solution of the discretized heat problem 13.154–13.156 (for Problem 13.5).

# PROBLEM 13.6

Use the routine PropagDiff (Listing 13.10), included in the files pde.py and, respectively, pde.h, to solve the diffusion equation

∂u/∂t = ∂/∂x ( D ∂u/∂x ),   x ∈ [0, L],   t > 0,   (13.157)

with L = 1, for a stack of three homogeneous layers occupying the intervals [0, x1), [x1, x2), and [x2, L], with x1 = 0.4L and x2 = 0.6L. Consider the nominal values of the diffusion coefficient D1 = D3 = 0.1 in the middle of the outer layers and D2 = 0.001 in the middle of the inner layer, and use the continuous functional dependence

D(x) = D1 + (D2 − D1) f_sw(x)   (13.158)

to switch smoothly between D1 and D2. The switch function f_sw(x) is defined by

f_sw(x) = [ 1 + exp( (|x − c| − w)/d ) ]^{−1},