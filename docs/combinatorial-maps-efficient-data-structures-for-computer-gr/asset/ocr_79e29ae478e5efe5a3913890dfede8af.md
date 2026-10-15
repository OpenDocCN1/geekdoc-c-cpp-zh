# Algorithm 55: isContractibleNGMap(gm,d,i): test if an i-cell is contractible for n-Gmaps

```
Input: gm: an n-Gmap;
    d ∈ gm.Darts: a dart;
    i ∈ {0,...,n}.
Output: True iff c_i(d) is contractible.
1 if i = 0 then return false;
2 if i = 1 then return true;
3 foreach dart d' ∈ c_i(d) do
4   if d'.Alphas[i - 2].Alphas[i - 1] ≠ d'.Alphas[i - 1].Alphas[i - 2]
5     then
6       return false;
7 return true;
```

# Algorithm 56: contractNGMap(gm,d,i): contract an i-cell for n-Gmaps

```
Input: gm: an n-Gmap;
    d ∈ gm.Darts: a dart such that c_i(d) is contractible;
    i ∈ {1,...,n}.
Result: Contract the i-cell c_i(d).
1 ma ← reserveMarkNGMap(gm);
2 mark all the darts in c_i(d) for ma;
3 foreach dart d' ∈ c_i(d) do
4   d1 ← d'.Alphas[i];
5   if not isMarkedNGMap(d1,ma) then
6     d2 ← d'.Alphas[i - 1].Alphas[i];
7     while isMarkedNGMap(d2,ma) do
8       d2 ← d2.Alphas[i - 1].Alphas[i];
9     d1.Alphas[i] ← d2;
10 foreach dart d' ∈ c_i(d) do
11   remove d' from gm.Darts;
12 freeMarkNGMap(gm,ma);
```