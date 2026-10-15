# Algorithm 57: isContractibleNMap(cm,d,i): test if an i-cell is contractible for n-maps

```
Input: cm: an n-map;
        d ∈ cm.Darts: a dart;
        i ∈ {0, ..., n}.
Output: True iff c_i(d) is contractible.
1 if i = 0 then return false;
2 if i = 1 then return true;
3 foreach dart d' ∈ c_i(d) do
4     if d'.Betas[i − 2].Betas[i − 1] ≠ d'.Betas[i − 1].Betas[inv(i − 2)]
5     then
6         return false;
7 return true;
```

# Algorithm 58: contractNMap(cm,d,i): contract an i-cell for n-maps

```
Input: cm: an n-map;
        d ∈ cm.Darts: a dart such that c_i(d) is contractible;
        i ∈ {2, ..., n}.
Result: Contract the i-cell c_i(d).
1 ma ← reserveMarkNMap(cm);
2 mark all the darts in c_i(d) for ma;
3 foreach dart d' ∈ c_i(d) do
4     d1 ← d'.Betas[i];
5     if not isMarkedNMap(cm,d1,ma) then
6         d2 ← d'.Betas[i − 1].Betas[i];
7         while isMarkedNMap(cm,d2,ma) do
8             d2 ← d2.Betas[i − 1].Betas[i];
9         if d1 ≠ cm.null_dart then
10            if d2 ≠ cm.null_dart then
11                d1.Betas[i] ← d2;
12            else
13                d1.Betas[i] ← cm.null_dart;
14        else
15            if d2 ≠ cm.null_dart then
16                d2.Betas[i] ← cm.null_dart;
17 foreach dart d' ∈ c_i(d) do
18     remove d' from cm.Darts;
19 freeMarkNMap(cm,ma);
```