Clearly, all the work done inside the loop takes O(1) per iteration, so the analysis requires determining the number of times around the loop. The loop starts with high - low = N - 1 and finishes with high - low >= 1. Every time through the loop, the value high - low must be at least halved from its previous value; thus, the number of times around the loop is at most floor(log(N - 1)) + 2. (As an example, if high - low = 128, then the maximum values of high - low after each iteration are 64, 32, 16, 8, 4, 2, 1, 0, -1.) Thus, the running time is O(log N). Equivalently, we could write a recursive formula for the running time, but this kind of brute-force approach is usually unnecessary when you understand what is really going on and why.

Binary search can be viewed on our first data-structure implementation. It supports the contains operation in O(log N) time, but all other operations (in particular, insert) require O(N) time. In applications where the data are static (i.e., insertions and deletions are not allowed), this could be very useful. The input would then need to be sorted once, but afterward accesses would be fast. An example is a program that needs to maintain information about the periodic table of elements (which arises in chemistry and physics). This table is relatively stable, as new elements are added infrequently. The element names could be kept sorted. Since there are only about 118 elements, at most eight accesses would be required to find an element. Performing a sequential search would require many more accesses.

# Euclid's Algorithm

A second example is Euclid's algorithm for computing the greatest common divisor. The greatest common divisor (gcd) of two integers is the largest integer that divides both. Thus, gcd(50, 15) = 5. The algorithm in Figure 2.10 computes gcd(M, N), assuming M >= N. (If N > M, the first iteration of the loop swaps them.)

The algorithm works by continually computing remainders until 0 is reached. The last nonzero remainder is the answer. Thus, if M = 1,989 and N = 1,590, then the sequence of remainders is 399, 393, 6, 3, 0. Therefore, gcd(1989, 1590) = 3. As the example shows, this is a fast algorithm.

As before, estimating the entire running time of the algorithm depends on determining how long the sequence of remainders is. Although log N seems like a good answer, it is not at all obvious that the value of the remainder has to decrease by a constant factor,

```
1 long long gcd( long long m, long long n )
2 {
3 while( n != 0 )
4 {
5 long long rem = m % n;
6 m = n;
7 n = rem;
8 }
9 return m;
10 }
```

Figure 2.10 Euclid's algorithm