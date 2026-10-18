```
```text
procedure SELECTBEACONS(i, N(i), PosSet(i))
    /* The algorithm finds a set of 3-tuples */
    /* from the neighbor set of a_i (beacons) */
    /* that satisfy the condition stated in corollary 1 */
    /* PosSet(i) = {p(j) : ∀j ∈ N(i), p(j) = co-ordinates of node j} */
    BSSet ← ∅;                                      ▷ Output set of chosen 3-tuples
    m ← |N(i)|;                                     ▷ Cardinality of N(i)
    TupleSet_i ← all possible 3-tuple combinations from set N(i);
    p ← |TupleSet_i|;                               ▷ Cardinality of TupleSet_i = (m choose 3)
    /* Let TupleSet_i^j ← jth tuple of TupleSet_i */
    for j = 1 to p do                              ▷ Consider jth tuple
        for k = 1 to 3 do
            /* Choose the pivot beacon */
            B_1 ← TupleSet_i^j(k);                  ▷ pivot = kth node of jth tuple
            /* Let B_2 and B_3 be the other 2 nodes of TupleSet_i^j */
            L_12 ← line joining points p(B_1) and p(B_2) ▷ for pivot and B_2
            L_13 ← line joining points p(B_1) and p(B_3) ▷ for pivot and B_3
            theta ← angle between L_12 and L_13             ▷ theta = ∠B_2B_1B_3
            if theta ≥ π/4 and theta ≤ π/2 then
                /* Add the jth 3-tuple to the set */
                /* of beacons that can be used to compute */
                /* location of node i, i.e., BSSet */
                BSSet ← BSSet ∪ TupleSet_i^j;
                break;                              ▷ go for next tuple
            end if
        end for
    end for
end procedure
```
```