Step n-1: Finally at the n-1th comparison, compare A1 and A2 and interchange so that A1<A2. After the n-1 comparisons the list will be in the sorted order. Algorithm 16.1 is the algorithm for bubble sort.

# Algorithm 16.1: BUBBLE SORT (DATA, N)

```
//Here DATA is an array with N elements
1. Repeat 2 and 3 steps for K=1 to N-1
2. Set PTR=1 // initializing pass pointer PTR
3. Loop until PTR=N-K
3. Check whether DATA [PTR] >DATA [PTR+1] then
2. Swap (DATA [PTR] , DATA [PTR+1])
3. Set PTR=PTR+1
4. End loop
5. End
```

# Example 16.1

Let A be an array with the elements 23 15 72 58 66 32 31 70 to be sorted. Figure 16.1 shows various steps in bubble sort.

Pass 1:Compare A1 and A2:
23 > 15, so interchange as follows:
23 15 72 58 66 32 31 70
Compare A2 and A3:
23 < 72, the elements are in order:
15 23 72 58 66 32 31 70
Compare A3 and A4:
72 > 58, so interchange as follows:
15 23 58 72 66 32 31 70
Compare A4 and A5:
72 > 66, so interchange as follows:
15 23 58 66 72 32 31 70
Compare A5 and A6:
72 >32, so interchange as follows:
15 23 58 66 32 72 31 70
Compare A6 and A7:
72 > 31, so interchange as follows:
15 23 58 66 32 31 72 70
Compare A7 and A8:
72 > 70, so interchange as follows:
15 23 58 66 32 31 70 72
At the first pass, the largest elements in the list is placed in the nth position and it takes (n-1) comparisons.