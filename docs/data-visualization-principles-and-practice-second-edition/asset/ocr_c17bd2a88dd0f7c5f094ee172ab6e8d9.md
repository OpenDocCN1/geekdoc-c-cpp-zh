![](bbox=[0.26, 0.13, 0.89, 0.3])

Figure 8.17. Loop subdivision cases.

1. New internal vertex: For a new internal vertex \( v' \) added half-way an edge \( e = (v_1, v_2) \), where \( e \) is not on the boundary of \( G \), \( v' \) is computed by linear interpolation of the coordinates of \( v_1 \) and \( v_2 \) and of the two vertices \( v_A \) and \( v_B \) of the triangles \( T_A \) and \( T_B \) from \( G \) which share \( e \), as follows (see also Figure 8.17(a)):

\[
v' = \frac{3}{8}v_1 + \frac{3}{8}v_2 + \frac{1}{8}v_A + \frac{1}{8}v_B.
\] (8.9)

2. Existing internal vertex: Existing vertices \( v \) which are not on \( G \)’s boundary (Figure 8.17(b)) are moved to a new position \( v' \) by linearly interpolating the positions of \( v \) and of all \( n \) vertices \( v_i \) which are connected to \( v \) by triangle edges in \( G \), as follows:

\[
v' = (1 - n\beta)v + \sum_{i=1}^n \beta v_i.
\] (8.10)

The interpolation factor \( \beta \) is set to \( \frac{3}{8} \) if \( n > 3 \), and to \( \frac{3}{16} \), if \( n = 3 \).

3. New boundary vertex: New vertices \( v' \) added on boundary edges \( e = (v_1, v_2) \) of \( G \) (Figure 8.17(c)) are computed simply by averaging the edge’s endpoints:

\[
v' = \frac{1}{2}v_1 + \frac{1}{2}v_2.
\] (8.11)

4. Existing boundary vertex: Finally, existing vertices \( v \) on boundary edges \( e = (v_1, v_2) \) (Figure 8.17(d)) are moved to new locations \( v' \) via the following linear interpolation:

\[
v' = \frac{1}{8}v_1 + \frac{1}{8}v_2 + \frac{6}{8}v.
\] (8.12)