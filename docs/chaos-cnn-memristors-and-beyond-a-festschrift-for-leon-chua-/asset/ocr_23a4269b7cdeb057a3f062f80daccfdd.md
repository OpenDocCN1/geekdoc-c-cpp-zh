![](bbox=[0.07, 0.11, 0.45, 0.48])

Fig. 2. Chaotic saddle for the Hénon map x_{n+1} = 6 - 0.4y_n - x_n^2, y_n = x_n.

main properties that would allow us to introduce the extended safe sets in a natural way.

Basically the safe sets are a set of curves that are placed in the square where is located the horseshoe map. We can see the form of different S^k safe sets in the Hénon map with escaping dynamics in Fig. 3. As we can see in that figure it is possible to group these curves using a specific order that we denote as k.

Bearing this graphical idea of safe sets in mind we can already define the main properties for the curves that are part of S^k (the safe set of order k.):

+   - S^k consist of 2^k vertical curves.
+   - Any vertical curve of S^k has two adjacent vertical curves of S^{k+1} closer to it than any other curve of S^k.
+   - The maximum distance between any of the 2^k curves of S^k and its two adjacent curves of S^{k+1}, denoted as δ_k, goes to zero as k → ∞.
+   - All the curves of a S^k set can be grouped in pairs. Each pair would be composed of the two closest curves.

The algorithm to find the adequate safe set in a system with escapes make use of the inverse of the horseshoe map. The procedure consists of making backward iterations (applying the inverse map) of a straight line centered in the square as we can see in Fig. 4. Making these iterations and computing their intersections with the square, we easily obtain all the curves that are part of a particular S^k, where

the order of the safe set corresponds to the number of iterations. Thus, it is possible to obtain the adequate safe set S^k that makes possible to avoid escapes even with a control smaller than the noise.

To properly quantify the properties of the partial control technique we need to define three parameters to establish the condition of a control smaller than the noise for a particular S^k:

+   - The first is the curve, ζ_i, that represents the middle distance in a particular pair of curves for a given S^k set.
+   - The second is the distance, δ_max(i), from the two points of that pair whose distance to ζ_i is maximum.
+   - The third is the distance, δ_min(i), from the two points of that pair whose distance to ζ_i is minimum.

We can visualize these parameters in Fig. 5 where we have plotted all of them for the two pairs of curves present in the S^2 set.

If we label as δ*_max as the largest δ_max(i) among all the pairs of curves, then it is easy to understand that the condition to have a control smaller than the noise is that ξ0 > δ*_max.

```
ξ0 > δ*_max. (3)
```

When this condition is satisfied, we can also compute the maximum control present in the system if we consider δ*_min as the smallest of all the δ_min among all the pairs of curves. Then we have that u0 = max{δ*_max, ξ0 - δ*_min}. (4)

# 4. Escape Time Sets

In order to define what is a extended safe set, it is necessary to review the idea of escape time of a trajectory starting in a region Q where exists a escaping dynamics. A point has a escape time n if the number of iterations that are needed to leave Q is n.

Using the idea of escape time it is possible to group all the points in the square Q in what we call T^n sets. We denote as T^n sets the sets of points in a square with a horseshoe dynamics, that stay inside the square under n iterations or more, that is: T^n = {p ∈ Q / f^n(p) ∈ Q}. (5)