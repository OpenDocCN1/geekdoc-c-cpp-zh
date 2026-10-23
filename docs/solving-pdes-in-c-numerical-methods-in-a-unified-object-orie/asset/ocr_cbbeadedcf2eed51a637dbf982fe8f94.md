# 5.30 The Rabin–Miller Test

A much more reliable test is indeed the Rabin–Miller test [51], [58]. This test checks whether a given odd number n > 3 is probably prime or not.

The test is defined as follows. First, factorize n − 1 in the form

n − 1 = 2^r s

where s is odd. (Because n is odd, n − 1 is even, so r > 0.) Then, pick some integer number a that satisfies 1 < a < n − 1. We say that the test is passed if either

a^s ≡ 1 mod n

or

a^{2^j s} ≡ −1 mod n

for some 0 ≤ j < r. Otherwise, the test is not passed.

The above test is based on the formula

a^{2^r s} − 1 = (a^{2^{r−1} s} − 1)(a^{2^{r−1} s} + 1) = (a^{2^{r−2} s} − 1)(a^{2^{r−2} s} + 1)(a^{2^{r−1} s} + 1) = (a^{2^{r−3} s} − 1)(a^{2^{r−3} s} + 1)(a^{2^{r−2} s} + 1)(a^{2^{r−1} s} + 1) = ⋯ = (a^s − 1)(a^s + 1)(a^{2 s} + 1)(a^{2^2 s} + 1)⋯(a^{2^{r−1} s} + 1).

The present test is indeed stricter than the original naive test: it requires that n divides not only a^{2^r s} − 1 but also one particular factor of it in the above factorization.

If n is prime, then this is indeed the case. After all, Fermat’s little theorem guarantees that n divides a^{2^r s} − 1. Furthermore, since n is prime, it must also divide one of the factors in the above factorization.

If, on the other hand, n is not prime, then it may still divide a^{2^r s} − 1, so the original naive test may mislead us to think that n is prime. Still, n may fail to pass the present stricter test. For example, n may be written as the product of two factors, each of which divides a different factor in the above factorization of a^{2^r s} − 1. In this case, the Rabin–Miller test is not passed, which indicates that n is not prime, as required.

In summary, passing the test is a necessary condition for n being prime. However, it is not a sufficient condition. In fact, there exists an n that is not prime, yet does pass the test for several a’s between 2 and n − 2. Such an a is called a liar, because it misleads us into thinking that n is prime. Fortunately, at most 25% of the a’s between 2 and n − 2 are liars [58]. Therefore, if a is picked randomly between 2 and n − 2, then the probability that the test would be passed is at most 1/4.

Thus, the probability that k independent tests would all mislead us to think that n is prime is as small as

4^{−k}.

For k = 10, for example, this probability is as small as

4^{−10} = 2^{−20} = 1024^{−2} ≤ 10^{−6}.