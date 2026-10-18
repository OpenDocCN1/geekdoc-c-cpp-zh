540 Mbps), the pulse width would be 5 to 1.85 ns, which translates to 1.5 to 0.555 meter for $c\tau_{uv}$ in Equation (4.1).

# 4.3  Estimation of Location Error

Assume that the location of a node $u$ is obtained through triangulation, using its neighboring beacons whose locations are already known. The error in the estimated position of node $u$ can arise from:

+   1. Uncertainties in the locations of the beacon nodes used for triangulating the location of node $u$.
+   2. Errors in ranging; NLOS errors are dominant.

# 4.3.1  Error due to Ambiguity in Node Coordinates

We first consider the case when the positions of the beacon nodes are not known accurately. Let us consider two beacon nodes $B_1$ and $B_2$ as in Figure 4.2, with corresponding estimated ranges as $r_1$ and $r_2$, respectively. Let $T$ represent the computed position of node $u$. Let $S$ be the foot of the normal drawn from $T$ to the line joining $B_1$ and $B_2$, with $d_1$ and $d_2$ being the distances of $S$ from $B_1$ and $B_2$, respectively. Let $d=d_1+d_2$. Then the coordinates of $S$ are $(d_1,0)$ and that of $T$ are $(d_1,\sqrt{r_1^2-d_1^2})$ with respect to the origin at $B_1(0,0)$ and considering the x-axis along $B_1B_2$.

If there is some error in the positional estimates of the beacon nodes, each of $B_1$ and $B_2$ can be taken anywhere within a circle of radius $\epsilon$ with $B_1$ and $B_2$ as centers as shown in Figure 4.3 (note that $B_1$ and $B_2$ are assumed to be the actual positions