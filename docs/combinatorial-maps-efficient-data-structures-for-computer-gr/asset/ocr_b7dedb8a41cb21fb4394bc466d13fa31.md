and $o_{d'} = \langle \alpha_0,\ldots,\alpha_{i-2},\alpha_{i+2},\ldots,\alpha_n\rangle(d')$. During the main loop, for each pair of darts pointed by it and it’, we consider all the darts in the neighborhood of it that are already considered. Indeed, we already have built the isomorphism between these darts through the associative array $f$, and we need to test if the local property of the $i$-sewable operation is satisfied (i.e. $f(\alpha_j(\mathrm{it})) = \alpha_j(\mathrm{it}')$, with $f(\mathrm{it}) = \mathrm{it}'$). When it is not the case, we directly return false as we know that the two darts $d$ and $d'$ are not $i$-sewable. Otherwise we continue the main loop until finishing at least one iterator. If only one iterator has finished, the two darts are not $i$-sewable (the two orbits do not have the same number of darts); otherwise, they are $i$-sewable, and we return true.

The complexity of the $i$-sewable algorithm is linear in the number of darts $\#d$ in the smaller orbit among $o_d$ and $o_{d'}$ times $\log \#d$. Indeed, we stop the main loop as soon as one iterator has reached its end position, and all operations are atomic except the access to an element in the associative array which is in log, and the inner loop (line 8) is bounded by $n$ which is a constant.

The $i$-sew operation is given in Algorithm 20, for $i \in \{0,\ldots,n\}$. This algorithm follows directly the definition of the $i$-sew operation (see Def. 19 page 91). The main loop consists to run through the two orbits $o_d = \langle \alpha_0,\ldots,\alpha_{i-2},\alpha_{i+2},\ldots,\alpha_n\rangle(d)$ and $o_{d'} = \langle \alpha_0,\ldots,\alpha_{i-2},\alpha_{i+2},\ldots,\alpha_n\rangle(d')$, and put in relation all pairs of darts by $\alpha_i$.

```
**Algorithm 20:** `sewNGMap(gm,d,d’,i)`: i-sew two darts for $n$-Gmaps

**Input:** gm: an $n$-Gmap;

$d,d' \in$ gm.Darts: two i-sewable darts;

$i \in \{0,\ldots,n\}$.

**Result:** i-sew darts d and d’.

```text
1  it ← generic iterator(gm,d,(0,...,i−2,i+2,...,n));
2  it’ ← generic iterator(gm,d’,(0,...,i−2,i+2,...,n));
3  while it is not to its end do
4      it.Alphas[i] ← it’;
5      it’.Alphas[i] ← it;
6      advance it to its next position;
7      advance it’ to its next position;
```
```

The key point of this algorithm is the use once again of the two generic iterators $(\mathrm{gm},d,(0,\ldots,i-2,i+2,\ldots,n))$ and $(\mathrm{gm},d',(0,\ldots,i-2,i+2,\ldots,n))$ to iterate through the two orbits by using the same $\alpha$ links. Since we know that $d$ and $d'$ are $i$-sewable, and since the generic iterator uses the indexes given in the sequence in the same order, at each step of the while loop, the two iterators point to two darts in relation by isomorphism $f$ of Def. 19. For this reason, we only need to put the two pointed darts in relation by $\alpha_i$, then move the two iterators to their next positions. Note that the relation is done in both directions as $\alpha_i$ is an involution. The algorithm ends when the two iterators reach their end positions.