To find the probability mass function $f$ which is invariant, let $f_i$ be the probability of state $i$ and $\mathbf{f} = (f_1, f_2, f_3)$. We need to solve $\mathbf{f}P = \mathbf{f}$,

$$\frac{1}{2}f_1 + f_3 = f_1, \\ \frac{1}{2}f_1 + \frac{1}{2}f_2 = f_2, \\ \frac{1}{2}f_2 = f_3.$$

which gives $f_1 = f_2 = 2f_3$. The probabilities also need to sum to one, i.e. $f_1 + f_2 + f_3 = 1$. With this, $\mathbf{f} = (2/5, 2/5, 1/5)$ describes the invariant distribution.

The other direction, i.e. constructing a Markov chain which is invariant for a given distribution $\mathbf{f}$, has more degrees of freedom, since the transition matrix has nine entries under the constraint that all rows have to sum to one. Let $\mathbf{f} = (f_1, f_2, f_3)$ define the probabilities of the random variable being in state 1, 2 or 3 respectively. The property of detailed balance leads to three equations,

$p_{12}f_1 = p_{21}f_2 \\ p_{13}f_1 = p_{31}f_3 \\ p_{23}f_2 = p_{32}f_3.$

The diagonal elements $p_{11}, p_{22}$, and $p_{33}$ can be determined, once the off-diagonal elements are chosen by using

$$\sum_{j=1}^3 p_{ij} = 1,$$

for $i = 1, 2, 3$.

More specifically, let $\mathbf{f} = (1/10, 2/5, 1/2)$. The detailed balance equations are

$$\frac{1}{10}p_{12} = \frac{2}{5}p_{21} \\ \frac{1}{10}p_{13} = \frac{1}{2}p_{31} \\ \frac{2}{5}p_{23} = \frac{1}{2}p_{32}.$$

Because we have some freedom of choice, we can set $p_{12} = 1$. This implies $p_{21} = 1/4$. It is not possible to set $p_{21} = 1$, since this would lead to a value greater than 1 for $p_{12}$. Since the probabilities in a row have to sum to one, we have $p_{11} = p_{13} = 0$. The second equation then leads to $p_{31} = 0$ as well. This has determined the first row and column of the transition matrix. Again using our freedom of choice, we set $p_{23} = 3/4$, which implies $p_{22} = 0$. The last equation determines $p_{32} = 2(3/4)(2/5) = 3/5$. Lastly $p_{33} = 2/5$, since the last row has to sum to one, and thus

$$P = \begin{pmatrix} 0 & 1 & 0 \\ \frac{1}{4} & 0 & \frac{3}{4} \\ 0 & \frac{3}{5} & \frac{2}{5} \end{pmatrix}.$$