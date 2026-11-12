As before, this lemma immediately implies that the algorithm RESEAT is 2-competitive, as desired.

# Algorithm 17 ReSeat Linear Time Algorithm

```
1: function FAST-RESEAT(G[1...m], n)
2:     admitted ← 0
3:     remaining ← n
4:     for i ← 1 to m do
5:         if G[i] ≥ n/2 and G[i] ≤ remaining then
6:             ADMIT(i)
7:             admitted ← admitted + G[i]
8:             remaining ← remaining − G[i]
9:         end if
10:    end for
11:    for i ← 1 to m do
12:        if G[i] ≤ remaining then
13:            ADMIT(i)
14:            admitted ← admitted + G[i]
15:            remaining ← remaining − G[i]
16:        end if
17:    end for
18:    return admitted
19: end function
```

The argument showing this algorithm is correct is essentially the same as the proof in third part. In particular, we again show the same lemma about the number of people seated.

# Lemma 3

Algorithm FAST-RESEAT either admits all groups of size ≤ n, or it admits ≥ n/2 people.

**Proof** Assume algorithm FAST-RESEAT does not admit all groups of size ≤ n. That is, there is some group gᵢ of size ≤ n that FAST-RESEAT does not admit.

There are two cases to consider. First, assume that gᵢ ≥ n/2. Then, since the algorithm first considers all groups of size ≥ n/2, we know that if gᵢ was rejected, it must have admitted some group of size ≥ n/2; otherwise, group gᵢ would have been admitted. Therefore, we can conclude that the algorithm seats ≥ n/2 people, as required.

For the second case, assume that gᵢ < n/2. If gᵢ is not admitted, we can conclude that gᵢ > remaining. That is, remaining < gᵢ < n/2.