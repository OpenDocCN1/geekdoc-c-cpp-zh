The following is a lower bound on the minimum number of channels needed for the solution of a given channel assignment problem $P$ from Gamst [42].

**Result 1.** *(Lemma 9 in [42]):* Let $P=(X,W,C)$ be a channel assignment problem (CAP), and assume there exists a $(v,v')$-complete subset pair $(Q,Q')$ of $X$ such that

$$c_{ij}\ge v'>v,\qquad\text{for all }i\in Q'\text{ and }j\in Q.$$ \tag{3.1}

If $$\sum_{i\in Q\setminus Q'}w_i>0,$$

let

$$L_1=1+v'\sum_{i\in Q'}w_i+v\left(\sum_{i\in Q\setminus Q'}w_i-1\right).$$

Then, $S_0(P)\ge L_1$.

Note that, Result 1 is particularly useful when applied to combinations of co-channel ($v=1$) and adjacent channel ($v'=2$) constraints (here represented by $s_2=1$ and $s_1=2$, respectively)[42]. Besides that, Result 1 is of little practical use due to the difficulty of finding a $(v,v')$-complete subset pair satisfying condition (3.1) that each cell in $Q'$ is at least $v'$-compatible with every cell in $Q$ [7]. Motivated by this observation, in [7], Tcha et al. derived a new lower bound $L_2$ for $P$, when the strict condition (3.1) is relaxed by devising a procedure of *frequency insertion* which allows lower-than-$v'$-compatibility for some cell pairs between $Q'$ and $Q$.

**Result 2.** *(Theorem 2 in [7]):* Let $P=(X,W,C)$ be a CAP having a $(v,v')$-complete subset pair $(Q,R)$ of $X$ with a maximal $v'$-complete subset $R$ of $Q$, from which a CAP $P'=(X,W',C')$ is defined, wherein $W'=(w'_i)$ and $C'=(c'_{ij})$ are given as