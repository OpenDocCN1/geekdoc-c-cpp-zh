U3: The method can be used to interpolate a function as well as its first and second derivatives.

We are assuming that the function to be approximated is smooth (see Ahlberg, Nilson and Walsh, 1967 for the mathematical details). In a sense we see the cubic spline as a surrogate for the function that we are investigating.

# 13.5.2 Caveat: Cubic Splines with Sparse Input Data

Cubic splines are well behaved for many kinds of applications but they can overshoot and produce spurious negative values, especially for non-equidistant data. This problem manifests itself in yield curve construction. An example is (Duffy and Germani, 2013):

```
std::vector<double> t{0.1,1.0,4.0,9.0,20.0,30.0};    // Time in years
std::vector<double> r{0.081,0.07,0.044,0.07,0.04,0.03};  // Interest rate
```

In these cases other methods are better, for example the Hagan–West, Akima and Hyman methods (Duffy and Germani, 2013; Hagan and West, 2006, 2008).

We give a brief mathematical explanation of why cubic splines fail under certain circumstances. To this end, we concentrate on the constraints on the distribution of the mesh values. Let {Δ_k}, k = 0, 1, 2, ... be a sequence of meshes consisting of N_k subintervals on the interval [a, b] defined by:

Δ_k : a = x_{k,0} < x_{k,1} < ⋯ < x_{k,N_k} = b.

We define the norm of Δ_k as:

‖Δ_k‖ = max_{1≤j≤N_k} (h_{k,j})   where   h_{k,j} = x_{k,j} − x_{k,j−1},   j = 1, …, N_k.

We are interested in sequences {Δ_k} for which ‖Δ_k‖ → 0 as k → ∞. We also require that:

R_{Δ_k} ≡ max_{1<j≤N_k} ‖Δ_k‖ / h_{k,j} ≤ β < ∞.   (13.39)

This inequality states that the ratio of the largest subinterval and the smallest subinterval is bounded. The inequality occurs in many branches of numerical analysis.

As an example, consider the mesh {1,2,3,3.1,5.1,6,7,8} that occurs in yield curve construction. The mesh sizes are {1,1,0.1,2,0.9,1,1} and hence Δ = 2, R_Δ = 20 (we have dropped the dependence on k).

The importance of constraint (13.39) lies in the fact that cubic splines produce approximations to smooth functions. The following theorem is proved in Ahlberg, Nilson and Walsh (1967, pp. 29–34):

# Theorem 1. Let f(x) be of class C³[a,b] (f and its first three derivatives are continuous on the interval [a, b]). Assume that lim_{k→∞}‖Δ_k‖ = 0 and that the mesh Δ_k satisfies constraint