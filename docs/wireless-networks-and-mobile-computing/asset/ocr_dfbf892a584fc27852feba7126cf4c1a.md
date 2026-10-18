of Minkowski’s sum of $R'_{u_{j-1}}$ and a circle of radius $r_{u_{j-1},u_j}$ (range value between nodes $u_{j-1}$ and $u_j$) with center at the origin, we see that for any $j$, $1 \leq j \leq k$, two possible cases may arise:

+   Case 1: A line segment (arc) in $E^{u_j}_{u_0,u_1\ldots u_{j-1}}$ is parallel to some line segment (arc) in $E^{u_{j-1}}_{u_0,u_1\ldots u_{j-2}}$ (for $j>1$) or in $R_{u_0}$ (for $j=1$).

+   Case 2: An arc in $E^{u_j}_{u_0,u_1\ldots u_{j-1}}$ is
+   
+   (a) not parallel to any arc in $E^{u_{j-1}}_{u_0,u_1\ldots u_{j-2}}$ (for $j>1$) or in $R_{u_0}$ (for $j=1$),
+   
+   (b) an arc of a circle with radius $r_{u_{j-1},u_j}$, having center at one point on the region $R'_{u_{j-1}}$ which is the point of intersection of two different arcs or two different line segments or an arc and a line segment, at least one of which must be in $E^{u_{j-1}}_{u_0,u_1\ldots u_{j-2}}$ (for $j>1$) or in $R_{u_0}$ (for $j=1$).

This is illustrated in Figure 4.10 where the arcs $\alpha$ and $\beta$ on $R'_{u_{j-1}}$ and $R'_{u_j}$, respectively, are parallel to each other, while the arc $\gamma$ on $R'_{u_j}$ is derived from the point $Q$ on $R'_{u_{j-1}}$ (with $Q$ as center and a radius equal to $r_{u_{j-1},u_j}$). We also see from Figure 4.10 that for every point on $R'_{u_j}$, there exists a unique point on $R'_{u_{j-1}}$ from which this point was derived. Thus, for the point $T$ on $R'_{u_j}$, the corresponding point on $R'_{u_{j-1}}$ is $Q$, which is transitively derived from a point $P$ on $R_{u_0}$.

**Lemma 15.** Let $T$ be any point on $E^{u_j}_{u_0,u_1\ldots u_{j-1}}$, and $P$ be the corresponding point on $R_{u_0}$ from which $T$ was derived. The Euclidean distance $PT$ is always greater than or equal to the maximum of all $(r_{u_{j-1},u_j},\ \forall j,1\leq j\leq k)$.

*Proof.* We prove this by induction on $j$. The claim is trivially true for $j=1$. Suppose the claim is true for $j=1,2,\ldots,j-1$. For $j\geq1$, referring to Figure 4.10, the Euclidean distance $PQ$ is then greater than or equal to the maximum of $(r_{u_0,u_1}, r_{u_1,u_2},\ldots,r_{u_{j-2},u_{j-1}})$. If the point $T$ is on an arc or line segment in $E^{u_j}_{u_0,u_1\ldots u_{j-1}}$ parallel to an arc or line segment in $E^{u_{j-1}}_{u_0,u_1\ldots u_{j-2}}$, the Euclidean distance $PT =$