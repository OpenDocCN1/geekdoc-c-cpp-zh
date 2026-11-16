Let \( W \subset V \), then Proposition 2.14 can be easily modified to obtain:

# Proposition 2.15.

\( L^T(W) \le \left(2 - \frac{2}{|W|}\right) Z_2^W(W). \)

Proof. Let \( (x_e) \) be a feasible solution to LP2. If \( e \notin E(W) = \{(i, j) \mid i, j \in W\} \), this implies \( x_e = 0 \) and using Proposition 2.14 we prove the inequality. \(\square\)

# Performance Bounds

Let \( (z^*, x^*, Z_1^*) = ((z_i^*)_{i=1}^n, (x_e^*)_{e \in E}, Z_1^*) \) be the optimal solution to the linear programming relaxation of the GMSTP. Define

\(\widehat{x}_e = \rho x_e^*\)
\(\widehat{z}_i = \begin{cases} 1 & \text{if } z_i^* \ge \frac{1}{\rho} \\ 0 & \text{otherwise.} \end{cases}\)

\( W^* = \left\{ i \in V \mid z_i^* \ge \frac{1}{\rho} \right\} = \{ i \in V \mid \widehat{z}_i = 1 \} \). Because we need only one vertex from every cluster, we delete extra vertices from \( W^* \) and consider \( W' \subset W^* \), such that \( |W'| = m \) and \( W' \) consists of exactly one vertex from every cluster.

Since LP1 is the linear programming relaxation of the problem IP1, we have

\( Z_1^* \le Z_1. \)

Now, let us show that \( (\widehat{x}_e)_{e \in E} \) is a feasible solution to LP3 with \( W = W' \). Indeed, \( \widehat{x}_e \ge 0 \) for all \( e \in E \), hence condition (2.47) is satisfied. Let \( S \subset V \) be such that \( W' \cap S \neq \emptyset \neq W' \setminus S \) and choose some \( i \in W' \cap S \). Hence \( \widehat{z}_i = 1 \) and \( z_i^* \ge \frac{1}{\rho} \). Then we have

\(\widehat{x}(\delta(S)) = \sum_{e \in \delta(S)} \widehat{x}_e = \rho \sum_{e \in \delta(S)} x_e^* \ge \rho z_i^* \ge \rho \frac{1}{\rho} = 1,\)

by definition of \( \widehat{x}_e \) and the fact that the \( (x^*) \) solve LP1. Hence the \( (\widehat{x}_e) \) satisfy constraint (2.44) in LP3. Therefore, for the approximation algorithm of the GMSTP APP, the following holds:

APP = \( L^T(W') \le \left(2 - \frac{2}{|W'|}\right) Z_2^W(W') = \left(2 - \frac{2}{|W'|}\right) Z_3^*(W') \)
\(\le \left(2 - \frac{2}{|W'|}\right) \sum_{e \in E} c_e \widehat{x}_e = \left(2 - \frac{2}{|W'|}\right) \rho \sum_{e \in E} c_e x_e^* = \left(2 - \frac{2}{|W'|}\right) \rho Z_1^* \)
\(\le \left(2 - \frac{2}{|W'|}\right) \rho Z_1 = \left(2 - \frac{2}{|W'|}\right) \rho \text{OPT}.\)

And since \( W' \subset V \), that is, \( m = |W'| \le |V| = n \), we have proved the following.