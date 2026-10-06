# Solutions to Chapter 8 | Recursion

in the set (the "yes" state) or (2) the element is not in the set (the "no" state). This means that each subset is a sequence of yeses/nos—e.g.,"yes, yes, no, no, yes, no"

This gives us 2^n possible subsets. How can we iterate through all possible sequences of "yes"/"no" states for all elements? If each "yes" can be treated as a 1 and each "no" can be treated as a 0, then each subset can be represented as a binary string.

Generating all subsets then just comes down to generating all binary numbers (that is, all integers). Easy!

```
ArrayList<ArrayList<Integer>> getSubsets(ArrayList<Integer> set) {
    new ArrayList<ArrayList<Integer>> allSubsets =
    int max = 1 << set.size();
    for (int i = 0; i < max; i++) {
        ArrayList<Integer> subset = new ArrayList<Integer>();
        int k = i;
        int index = 0;
        while ((k > 0) {
            if ((k & 1) > 0)nn                subset.add(set.get(index));
            k >>= 1;
            index++;
        }
        allSubsets.add(subset);
    }
    return allSubsets;
}
```