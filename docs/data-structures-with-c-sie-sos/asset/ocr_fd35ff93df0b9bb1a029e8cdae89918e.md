# Pattern Matching

3.18 For each of the following patterns P and texts T, find the number C of comparisons to find the INDEX of P in T using the “slow” algorithm, Algorithm 3.3:
(a) P = abc, T = (ab)^5 = ababababab (b) P = abc, T = (ab)^{2n}
(c) P = aaa, T = (abb)^3 = aabbaabbaabb (d) P = aaa, T = abaabbaaabbbaaaabbb

Recall that C = N_1 + N_2 + ... + N_k where N_k denotes the number of comparisons that take place in the inner loop when P is compared with W_K,

(a) Note first that there are
LENGTH(T) - LENGTH(P) + 1 = 10 - 3 + 1 = 8
substrings W_K. We have
C = 2 + 1 + 2 + 1 + 2 + 1 + 2 + 1 = 4(3) = 12
and INDEX(T, P) = 0, since P does not appear in T.

(b) There are 2n - 3 + 1 = 2(n - 1) subwords W_K. We have
C = 2 + 1 + 2 + 1 + ... + 2 + 1 = (n + 1)(3) = 3n + 3
and INDEX(T, P) = 0.

(c) There are 12 - 3 + 1 = 10 subwords W_K. We have
C = 3 + 2 + 1 + 1 + 3 + 2 + 1 + 1 + 3 + 2 = 19
and INDEX(T, P) = 0.

(d) We have
C = 2 + 1 + 3 + 2 + 1 + 1 + 3 = 13
and INDEX(T, P) = 7.

3.19 Suppose P is an r-character string and T is an s-character string, and suppose C(n) denotes the number of comparisons when Algorithm 3.3 is applied to P and T. (Here n = r + s.)
(a) Find the complexity C(n) for the best case.
(b) Prove that the maximum value of C(n) occurs when r = (n + 1)/4.

(a) The best case occurs when P is an initial substring of T, or, in other words, when INDEX(T, P) = 1. In this case C(n) = r. (We assume r <= s.)
(b) By the discussion in Sec. 3.7,
C = C(n) = r(n - 2r + 1) = nr - 2r^2 + r
Here n is fixed, so C = C(n) may be viewed as a function of r. Calculus tells us that the maximum value of C occurs when C' = dc/dr = 0 (here C' is the derivative of C with respect to r). Using calculus, we obtain:
C' = n - 4r + 1
Setting C' = 0 and solving for r gives us the required result.