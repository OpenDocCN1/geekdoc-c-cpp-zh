# Algorithm 19: sewableNGMap(gm,d,d′,i): test if two darts are i-sewable for n-Gmaps

Input: gm: an n-Gmap;
        d, d′ ∈ gm.Darts: two darts;
        i ∈ {0,…,n}.
Output: True iff d is i-sewable with d′.

```
1 if d = d′ or not isFreeNGMap(d,i) or not isFreeNGMap(d′,i) then
2   return false;
3 it ← generic iterator(gm,d,(0,…,i−2,i+2,…,n));
4 it′ ← generic iterator(gm,d′,(0,…,i−2,i+2,…,n));
5 f ← an empty associative array between darts;
6 while it is not to its end and it′ is not to its end do
7   f[it] ← it′;
8   foreach j ∈ {0,…,i−2,i+2,…,n} do
9     if it.Alphas[j] is defined in f and
10    f[it.Alphas[j]] ≠ it′.Alphas[j] then
11      return false;
12   advance it to its next position;
13   advance it′ to its next position;
14 if it is not to its end or it′ is not to its end then
15   return false;
16 return true;
```