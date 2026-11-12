which has the virtue that it reduces arbitrary partial sums to special ones, namely, those from 0 onwards.

If we introduce an abbreviation

$$x_k = \sum_{i=0}^{k-1} (p[i] - q[i]), k \ge 0$$

then

$$C(k,N) = (\forall h : 0 \le h < N : x_{k+h+1} \ge x_k)$$

Thanks to the fact that

$$x_N = \sum_{i=0}^{N-1} (p[i] - q[i]) = 0,$$

the condition C(k,N) can be simplified drastically.

$$C(k,N) : (\forall h : 0 \le h < N : x_h \ge x_k),$$

expressing that $x_k = \min(x_0,x_1,\ldots,x_{N-1})$.

We can capture the desired net effect of the program to be constructed as the computation of the set Z of pit numbers such that the relation

$$Z = \{ k \mid 0 \le k < N \land C(k,N) \}$$

is satisfied.

We propose to develop the program by sticking to the invariant

$$0 \le n \le N \land Z = \{ k \mid 0 \le k < n \land C(k,n) \}.$$

strengthened, for rather obvious reasons, with

$$xx = \min(x_0,x_1,\ldots,x_{n-1})$$

and

$$x = x_{n-1} = \left( \sum_{i=0}^{n-2} (p[i] - q[i]) \right)$$

respectively.

If, furthermore, the set Z is represented as

$$Z = \{ f[0], f[1], \ldots, f[l-1] \}.$$

in which f refers to an integer array and l is an integer, the program is readily constructed. The detailed derivation of it is, by now, left as an exercise.

The final program is: