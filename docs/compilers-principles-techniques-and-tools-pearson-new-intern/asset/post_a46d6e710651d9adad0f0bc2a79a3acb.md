
## 11.9. PIPELINING

permutable, we have a lot of freedom in how we wish to parallelize the code. The first pipeline scheme maps iteration [i, j] to processor i; the second maps iteration [i, j] to processor j. We can create alternative pipelines by mapping iteration [i, j] to processor c₀i + c₁j, provided c₀ and c₁ are positive constants. Such a scheme would create pipelines with delayed wavefronts between 90° and 180°, both exclusive.

### 11.9.5 General Theory

The example just completed illustrates the following general theory underlying pipelining: if we can come up with at least two different outermost loops for a loop nest and satisfy all the dependences, then we can pipeline the computation. A loop with k outermost fully permutable loops has k − 1 degrees of pipelined parallelism.

Loops that cannot be pipelined do not have alternative outermost loops. Example 11.56 shows one such instance. To honor all the dependences, each iteration in the outermost loop must execute precisely the computation found in the original code. However, such code may still contain parallelism in the inner loops, which can be exploited by introducing at least n synchronizations, where n is the number of iterations in the outermost loop.

```c
for (i = 0; i < 100; i++) {
    for (j = 0; j < 100; j++)
        X[j] = X[j] + Y[i,j];   /* (s1) */
    Z[i] = X[A[i]];              /* (s2) */
}
```

![](img/a29d16e454785bb105e96ef448ac07f6_871_0.png)

(a)

(b)

Figure 11.53: A sequential outer loop (a) and its PDG (b)

**Example 11.56:** Figure 11.53 is a more complex version of the problem we saw in Example 11.50. As shown in the program dependence graph in Fig. 11.53(b), statements s₁ and s₂ belong to the same strongly connected component. Because we do not know the contents of matrix A, we must assume that the access in statement s₂ may read from any of the elements of X. There is a true dependence from statement s₁ to statement s₂ and an antidependence from statement s₂ to statement s₁. There is no opportunity for pipelining either, because all operations belonging to iteration i in the outer loop must precede those in iteration i + 1. To find more parallelism, we repeat the parallelization process on the inner loop. The iterations in the second loop can be parallelized without synchronization. Thus, 200 barriers are needed, with one before and one after each execution of the inner loop. □

### 11.9.6 Time-Partition Constraints

We now focus on the problem of finding pipelined parallelism. Our goal is to turn a computation into a set of pipelinable tasks. To find pipelined parallelism, we do not solve directly for what is to be executed on each processor, like we did with loop parallelization. Instead, we ask the following fundamental question: What are all the possible execution sequences that honor the original data dependences in the loop? Obviously the original execution sequence satisfies all the data dependences. The question is if there are affine transformations that can create an alternative schedule, where iterations of the outermost loop execute a different set of operations from the original, and yet all the dependences are satisfied. If we can find such transforms, we can pipeline the loop. The key point is that if there is freedom in scheduling operations, there is parallelism; details of how we derive pipelined parallelism from such transforms will be explained later.

To find acceptable reorderings of the outer loop, we wish to find one-dimensional affine transforms, one for each statement, that map the original loop index values to an iteration number in the outermost loop. The transforms are legal if the assignment can satisfy all the data dependences in the program. The “time-partition constraints,” shown below, simply say that if one operation is dependent upon the other, then the first must be assigned an iteration in the outermost loop no earlier than that of the second. If they are assigned in the same iteration, then it is understood that the first will be executed after that of the second within the iteration.

An affine-partition mapping of a program is a legal time-partition if and only if for every two (not necessarily distinct) accesses sharing a dependence, say

$$\mathcal{F}_1 = \langle \mathbf{F}_1, \mathbf{f}_1, \mathbf{B}_1, \mathbf{b}_1 \rangle$$

in statement $s_1$, which is nested in $d_1$ loops, and

$$\mathcal{F}_2 = \langle \mathbf{F}_2, \mathbf{f}_2, \mathbf{B}_2, \mathbf{b}_2 \rangle$$

in statement $s_2$ nested in $d_2$ loops, the one-dimensional partition mappings $\langle C_1, c_1 \rangle$ and $\langle C_2, c_2 \rangle$ for statements $s_1$ and $s_2$, respectively, satisfy the time-partition constraints:

- For all $\mathbf{i}_1$ in $Z^{d_1}$ and $\mathbf{i}_2$ in $Z^{d_2}$ such that
    - a) $\mathbf{i}_1 \prec_{s_1,s_2} \mathbf{i}_2$,
    - b) $B_1 i_1 + b_1 \ge 0$,
    - c) $B_2 i_2 + b_2 \ge 0$, and
    - d) $F_1 i_1 + f_1 = F_2 i_2 + f_2$,

it is the case that $C_1 i_1 + c_1 \le C_2 i_2 + c_2$.

This constraint, illustrated in Fig. 11.54, looks remarkably similar to the space-partition constraints. It is a relaxation of the space-partition constraints in that if two iterations refer to the same location, they do not necessarily have to be mapped to the same partition; we only require that the original relative execution order between the two iterations is preserved. That is, the constraints here have \(\le\) where the space-partition constraints have \(=\).

![](img/a29d16e454785bb105e96ef448ac07f6_873_0.png)

Figure 11.54: Time-Partition Constraints

We know that there exists at least one solution to the time-partition constraints. We can map operations in each iteration of the outermost loop back to the same iteration, and all the data dependencies will be satisfied. This solution is the only solution to the time-partition constraints for programs that cannot be pipelined. On the other hand, if we can find several independent solutions to time-partition constraints, the program can be pipelined. Each independent solution corresponds to a loop in the outermost fully permutable nest. For instance, there is only one independent solution to the timing constraints extracted from the program in Example 11.56, where there is no pipelined parallelism. As another instance, there are two independent solutions to the SOR code example of Section 11.9.2.

**Example 11.57:** Let us consider Example 11.56, and in particular the data dependences of references to array \(X\) in statements \(s_1\) and \(s_2\). Because the access is not affine in statement s₂, we approximate the access by modeling matrix X simply as a scalar variable in dependence analysis involving statement s₂. Let (i,j) be the index value of a dynamic instance of s₁ and let i' be the index value of a dynamic instance of s₂. Let the computation mappings of statements s₁ and s₂ be (⟨C₁₁,C₁₂⟩,c₁) and (⟨C₂₁⟩,c₂), respectively.

Let us first consider the time-partition constraints imposed by dependences from statement s₁ to s₂. Thus, if i ≤ i', the transformed (i,j)th iteration of s₁ must be no later than the transformed i'th iteration of s₂; that is,

$$[ C_{11}\ C_{12} ] [ i ; j ] + c_1 \le C_{21} i' + c_2.$$

Expanding, we get

$$C_{11} i + C_{12} j + c_1 \le C_{21} i' + c_2.$$

Since j can be arbitrarily large, independent of i and i', it must be that \(C_{12} = 0\). Thus, one possible solution to the constraints is

$$C_{11} = C_{21} = 1 \quad \text{and} \quad C_{12} = c_1 = c_2 = 0.$$

Similar arguments about the data dependence from \(s_2\) to \(s_1\) and from \(s_2\) back to itself will yield a similar answer. In this particular solution, the ith iteration of the outer loop, which consists of the instance i of s₂ and all instances (i,j) of s₁, is assigned to timestep i. Other legal choices of C₁₁, C₂₁, c₁, and c₂ yield similar assignments, although there might be timesteps at which nothing happens. That is, all ways to schedule the outer loop require the iterations to execute in the same order as in the original code. This statement holds whether all 100 iterations are executed on the same processor, on 100 different processors, or anything in between. □

**Example 11.58:** In the SOR code shown in Fig. 11.50(a), the write reference X[j + 1] shares a dependence with itself and with the three read references in the code. We are seeking computation mapping (⟨C₁,C₂⟩,c) for the assignment statement such that

$$[ C_1\ C_2 ] [ i ; j ] + [ c ] \le [ C_1\ C_2 ] [ i' ; j' ] + [ c ]$$

if there is a dependence from (i,j) to (i',j'). By definition, (i,j) < (i',j'); that is, either i < i' or (i = i' ∧ j < j').

Let us consider three of the pairs of data dependences:

- 1. True dependence from write access X[j + 1] to read access X[j + 2]. Since the instances must access the same location, j + 1 = j' + 2 or j = j' + 1. Substituting j = j' + 1 into the timing constraints, we get

      $$C_1(i' - i) - C_2 \ge 0.$$
