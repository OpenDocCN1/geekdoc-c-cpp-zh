# Theorem 11.6.5 (Calderbank Bound) Let $C_0$ be a subcode of codimension $i \ge 1$ in a binary linear code $C$ of length $n$. Then

\(\rho(C_0) \le 2\rho(C) + 2^i - 1\).

Proof: Let H be a parity check matrix for C. We can add i rows to H to form a parity check matrix

\(H_0 = \begin{bmatrix} H \ H_1 \end{bmatrix}\)

for $C_0$. Let the $j$th column of $H_0$ be $h_0^j$ for $1 \le j \le n$.

Let \(\rho = \rho(C)\) and \(\rho_0 = \rho(C_0)\). If \(\rho_0 \le 2\rho + 1\), then (11.20) clearly holds. So assume that \(\rho_0 \ge 2\rho + 2\). There must be some syndrome $s_0^T$ of $C_0$ which is a sum of $\rho_0$ columns of $H_0$ but no fewer. By rearranging the columns of $H_0$, we may assume that

\(s_0^T = \sum_{j=1}^{\rho_0} h_0^j\).

Form the Kneser graph, $K(\rho_0, \rho+1)$. This graph has as vertex set $V$ the set of vectors in $\mathbb{F}_2^n$ of weight $\rho+1$. We write each vector $\mathbf{v} \in \mathbb{F}_2^n$ as $(\mathbf{v}', \mathbf{v}'')$, where $\mathbf{v}' \in \mathbb{F}_2^{\rho_0}$. We wish to establish a coloring $f$ of the vertices of $K(\rho_0, \rho+1)$. For every $\mathbf{v}' \in V$, there is an $\mathbf{x}_v \in C$ of distance at most $\rho$ from $(\mathbf{v}', \mathbf{0})$ as $\rho(C) = \rho$. For each $\mathbf{v}' \in V$ choose one such $\mathbf{x}_v \in C$ and define

\(f(\mathbf{v}') = H_1 \mathbf{x}_{\mathbf{v}'}^T\).

Notice that $f(\mathbf{v}') \in \mathbb{F}_2^i$. We first establish that $H_1 \mathbf{x}_{\mathbf{v}'}^T \neq 0$. Suppose $H_1 \mathbf{x}_{\mathbf{v}}^T = 0$. Then $H_0 \mathbf{x}_{\mathbf{v}}^T = \mathbf{0}$ as $H \mathbf{x}_{\mathbf{v}}^T = \mathbf{0}$ because $\mathbf{x}_v \in C$. Therefore,

\(H_0(\mathbf{v}', \mathbf{0})^T = H_0((\mathbf{v}', \mathbf{0}) - \mathbf{x}_v)^T\).

Because $wt(\mathbf{v}) = \rho+1$, the left-hand side of (11.22) is a combination of $\rho+1$ columns of $H_0$ from among the first $\rho_0$ columns of $H_0$, while the right-hand side of (11.22) is a combination of at most $\rho$ columns of $H_0$ as $wt((\mathbf{v}', \mathbf{0}) - \mathbf{x}_v) \le \rho$. Thus on the right-hand side of (11.21) we may replace $\rho+1$ of the columns of $H_0$ by at most $\rho$ columns of $H_0$ indicating that $\mathbf{s}_0^T$ is a linear combination of at most $\rho_0 - 1$ columns of $H_0$, which is a contradiction. This shows that $f(\mathbf{v}')$ is one of the $2^i - 1$ nonzero elements of $\mathbb{F}_2^i$.

We now establish that $f$ is indeed a coloring of $K(\rho_0, \rho+1)$. Let $\{\mathbf{v}', \mathbf{w}'\}$ be an edge of $K(\rho_0, \rho+1)$. We must show that $H_1 \mathbf{x}_{\mathbf{v}'}^T \neq H_1 \mathbf{x}_{\mathbf{w}'}^T$. Suppose that $H_1 \mathbf{x}_{\mathbf{v}'}^T = H_1 \mathbf{x}_{\mathbf{w}'}^T$. Then as $\mathbf{v}'$ and $\mathbf{w}'$ are in $V$, where $supp(\mathbf{v}')$ and $supp(\mathbf{w}')$ are disjoint, $wt(\mathbf{v}' + \mathbf{w}') = 2\rho + 2$. Additionally, the distance between $(\mathbf{v}' + \mathbf{w}', \mathbf{0})$ and $\mathbf{x}_v + \mathbf{x}_w$ is at most $2\rho$. Since $H_1(\mathbf{x}_v + \mathbf{x}_w)^T = \mathbf{0}$ and $H(\mathbf{x}_v + \mathbf{x}_w)^T = \mathbf{0}$ because $\mathbf{x}_v + \mathbf{x}_w \in C$, we have $H_0(\mathbf{x}_v + \mathbf{x}_w)^T = \mathbf{0}$. As in (11.22),

\(H_0(\mathbf{v}' + \mathbf{w}', \mathbf{0})^T = H_0((\mathbf{v}' + \mathbf{w}', \mathbf{0}) - (\mathbf{x}_v + \mathbf{x}_w))^T\).