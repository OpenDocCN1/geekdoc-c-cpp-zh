```
~~~
Algorithm 34 Celebrity Algorithm Brute Force
1: Input : set S of n people
2: Output : a celebrity, or _no celebrity_ if there is no celebrity.
3: for all A ∈ S do
4:     for all B ∈ S − {A} do
5:         if A knows B then
6:             Break out of inner loop
7:         else
8:             C ← A
9:         end if
10:    end for
11: end for
12: for all α ∈ S do
13:    if α does not know C then
14:        return “No Celebrity”
15:    end if
16:    return C
17: end for
~~~
```

This algorithm runs in O(n2) time. Can we do better? Yes, we can. The following algorithm is based on the observation that by asking a single question, we can eliminate a person as a possible celebrity. So, if I ask “Does A know B?” and the answer is “no”, then B cannot be a celebrity, because a celebrity must be known by everybody else. On the other hand, if the answer is “yes”, then A cannot be a celebrity because a celebrity knows nobody. Therefore, with a single question “Does A know B?”, we learn something no matter what the answer to the question is. This leads to this algorithm: