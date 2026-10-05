# # APPENDIX
# B

# # Solutions to Exercises

# ## Chapter 1: Algorithm Basics

+   1. The outer loop still executes O(N) times in the new version of the algorithm. When the outer loop's counter is $i$, the inner loop executes O(N - i) times. If you add up the number of times the inner loop executes, the result is N + (N-1) + (N-2) + ... + 1 = N(N-1) / 2 = ($N^2$-N) /2. This is still O($N^2$), although the performance in practice will probably be faster than the original version.
2. See Table B-1. The value *Infinity* means that the program can execute the algorithm for any practical problem size. The example program Ch01Ex02, which is available for download on the book's website, generates these values.

| TIME | LOG(n) | SQRT(n) | $n$ | $n^2$ | $2^n$ | $n!$ |
| --- | --- | --- | --- | --- | --- | --- |
| Second | Infinity | $1\times10^{12}$ | $1\times10^6$ | 1,000 | 20 | 10 |
| Minute | Infinity | $4\times10^{15}$ | $6\times10^7$ | 7,746 | 26 | 12 |
| Hour | Infinity | $1\times10^{19}$ | $4\times10^9$ | 60,000 | 32 | 13 |
| Day | Infinity | $7\times10^{21}$ | $9\times10^{10}$ | 293,936 | 36 | 14 |
| Week | Infinity | $4\times10^{11}$ | $6\times10^{11}$ | 777,689 | 39 | 15 |
| Year | Infinity | $1\times10^{27}$ | $3\times10^{13}$ | 5,617,615 | 45 | 17 |

**Table B-1: Maximum Problem Sizes That Run in Various Times**