
After the assignment to a peripheral node, to assign a channel to the central node, the minimum gap length would be $s_1$. And also we are to keep another gap of length $s_1$ before assigning a frequency to a peripheral node after the central node. Instead, it would be more economical to first complete the assignments of all the required channels to the peripheral nodes and then assign channels to the central node.

If, however, the minimum and maximum frequency channels are assigned to the central node, the lower bound on *minimum* $p$ as follows from the above discussion is $(\sum_{i=1}^{7} w_i-1)s_2+(s_0-s_2)(w_4-2)+2(s_1-s_2)$, $w_4$ being the demand of the central node 4.

*Case 2)* When $s_0 \ge (2s_1-s_2)$:

It would be more economical to assign to the central node after the assignment of a peripheral node, and after that to assign to a peripheral node from the central node.

If the minimum and maximum frequency channels are assigned to the central node, the lower bound on *minimum* $p$ would be $(\sum_{i=1}^{7} w_i-1)s_2+2(s_1-s_2)(w_4-2)+2(s_1-s_2)$.

It does not, however, necessarily mean that there always exists a conflict-free assignment of $G$ with the lower bound given above.

Several lower bounds on the minimum bandwidth requirement $S_0(P)$ for a given CAP $P$ have been described in [42, 7, 20] for non-homogeneous demands. These bounds are based on solving $CAPs$ which are simpler than $P$ defined in the following subsets of $X$ [7].

**Definition 1.** Let $v$ and $v'$ be two positive integers such that $v' > v$. Then,

+   - A subset $Q$ of $X$ is said to be $v$-complete if $c_{ij} \ge v$ for all $i,j \in Q$.
+   - A subset pair $(Q,Q')$ of $X$ is said to be $(v,v')$-complete if $Q$ is a $v$-complete subset of $X$ and $Q'$ is a $v'$-complete subset of $Q$.

The following is a lower bound on the minimum number of channels needed for the solution of a given channel assignment problem $P$ from Gamst [42].

**Result 1.** *(Lemma 9 in [42]):* Let $P=(X,W,C)$ be a channel assignment problem (CAP), and assume there exists a $(v,v')$-complete subset pair $(Q,Q')$ of $X$ such that

$$c_{ij}\ge v'>v,\qquad\text{for all }i\in Q'\text{ and }j\in Q.$$ \tag{3.1}

If $$\sum_{i\in Q\setminus Q'}w_i>0,$$

let

$$L_1=1+v'\sum_{i\in Q'}w_i+v\left(\sum_{i\in Q\setminus Q'}w_i-1\right).$$

Then, $S_0(P)\ge L_1$.

Note that, Result 1 is particularly useful when applied to combinations of co-channel ($v=1$) and adjacent channel ($v'=2$) constraints (here represented by $s_2=1$ and $s_1=2$, respectively)[42]. Besides that, Result 1 is of little practical use due to the difficulty of finding a $(v,v')$-complete subset pair satisfying condition (3.1) that each cell in $Q'$ is at least $v'$-compatible with every cell in $Q$ [7]. Motivated by this observation, in [7], Tcha et al. derived a new lower bound $L_2$ for $P$, when the strict condition (3.1) is relaxed by devising a procedure of *frequency insertion* which allows lower-than-$v'$-compatibility for some cell pairs between $Q'$ and $Q$.

**Result 2.** *(Theorem 2 in [7]):* Let $P=(X,W,C)$ be a CAP having a $(v,v')$-complete subset pair $(Q,R)$ of $X$ with a maximal $v'$-complete subset $R$ of $Q$, from which a CAP $P'=(X,W',C')$ is defined, wherein $W'=(w'_i)$ and $C'=(c'_{ij})$ are given as

[PAGE 126]

![](img/6578f6fc95ac71d2c7109e594d9df12f_126_0.png)

Here we consider another lower bound presented in [42] in the presence of co-site constraints ($s_0$).

**Result 3.** *(Lemma 10 in [42]):* Let $P=(X,W,C)$ be a CAP, $v$ be a positive integer, and $Q$ be a $v$-complete subset of $X$. Assume that $c_{ii}=k>v$ for all $i\in Q$. Furthermore, let

$$w=\max_{i\in Q} w_i$$

with $r$ cells in $Q$ having $w_i=w$.

If

$$L_0=\sum_{i\in Q}w_i,$$

$$L_1=v(L_0-1)+1,$$

$$L_2=k(m-1)+v(r-1)+1,$$

[PAGE 127]

$k=qv+v_0,\ 0\leq v_0<v,$

*then*

$S_0(P)\geq L_1,\quad \text{for }L_1-L_2\geq (v-v_0)(w-1),$

$S_0(P)\geq L_2,\quad \text{for }L_2-L_1\geq v_0(w-1),$

*and*

$S_0(P)\geq L_3=L_2+(L_0-r-q(w-1))(v-v_0),$

*in all other cases.*

Here, we consider another lower bound presented in [20] in the presence of co-site constraints.

# **Result 4.** *(Theorem 2 in [20]):* Let $P=(X,W,C)$ be a CAP and $Q$ be a 1-complete subset of $X$. Let $i\in Q$. Assume $c_{ii}=k>v'>1$ and there exists a subset of $Q$, $R$ such that

$i\notin R$

*and*

$c_{ii}\geq v',\quad \text{for all }j\in R.$

Furthermore, let $w_R=\sum_{j\in R}w_j$.

*If* $k-2v'+1\leq 0$

$S_0(P)\geq (w_i-1)k+1+w_R,$

[PAGE 128]

While solving an optimization problem using a genetic algorithm, the parameter set of the optimization problem must be coded as a finite-length string or chromosome over some finite alphabet \( Q \) [47]. A collection of \( M \) (finite) such strings or chromosomes is called a population. A simple genetic algorithm is composed of three basic operators: i) reproduction or selection, ii) crossover, and iii) mutation [47]. A genetic algorithm (GA) starts with an initial population (randomly generated) and in each iteration, a new (hopefully improved) population of the same size is generated from the current population by applying the above-mentioned operators on the strings of the current population. The newly generated population is then used to generate the next (possibly improved) population and so on.

Let \( S_b \) be the best string (with respect to the fitness value) of the population generated up to iteration \( t \). In the elitist model of genetic algorithm (EGA), if \( S_b \) or any string better than \( S_b \) is not in the population generated in iteration \( (t + 1) \), we include \( S_b \) in the \( (t + 1)$-th population [47]. We describe below this technique for solving the channel assignment problem as given in [29] which ensures that the population is improved in successive iterations.

[PAGE 129]

# 3.4.1 Problem Formulation

Let us assume that the channel assignment problem is represented by a CAP graph and the frequency separation constraints are given by the matrix $C=(c_{ij})$ as described in Section 3.1.2. Suppose the CAP graph has $n$ nodes. A random order of these nodes is considered a string $S$ or chromosome. For example, $S=((20),(21),(10),(11),(00))$ is a string corresponding to the CAP graph of Figure 3.1(a). Let $M$ be the population size (we have taken $M$ as an even integer). Let $cp$ be the crossover probability. We set $cp$ to a high value, say 0.95, in the algorithm.

![](img/6578f6fc95ac71d2c7109e594d9df12f_129_0.png)

**FIGURE 3.9:** Variation of mutation probability ($q$) with number of iterations ($t$)

Let $q$ be the mutation probability and $T$ be the total number of iterations. Usually, $T$ is a very large positive integer. We divide the total number of iterations into five equal intervals (assuming that $T$ is a multiple of 5) as $[0,T/5]$, $[T/5,2T/5]$, $[2T/5,3T/5]$, $[3T/5,4T/5]$ and $[4T/5,T]$. We start with a mutation probability of $q=0.5$ and then it is varied with the number of iterations as shown in Figure 3.9. The way in which the mutation probability is varied here is similar to that used in [48]. The reason for varying the mutation probability $q$ in this fashion is that we are to increase the value of $q$ to maintain the diversity of the

[PAGE 130]

population; similarly as the optimal string is approached, q is to be reduced. Figure 3.9 shows one such technique for varying q with the number of iterations.

The mutation probability at the t-th iteration is given by the following function.

```
Function m_probability(int t)
begin
W ← 5(1 - 0.5n)/(nT)
for i = 0 to 2 do
begin
V ← 2i + 1
V ← 2i + 1
if (t ≤ VT/5) do
begin
U ← t - (V - 1)T/5
U ← t - (V - 1)T/5
return (0.5 + WU)
return (0.5 + WU)
break
break
end;
end;
if (t ≤ (V + 1)T/5) do
begin
U ← (V + 1)T/5 - t
U ← (V + 1)T/5 - t
return (0.5 + WU)
return (0.5 + WU)
break
break
end;
end
end.
```

The fitness function Fit(S) used in the algorithm is described by the following function.
