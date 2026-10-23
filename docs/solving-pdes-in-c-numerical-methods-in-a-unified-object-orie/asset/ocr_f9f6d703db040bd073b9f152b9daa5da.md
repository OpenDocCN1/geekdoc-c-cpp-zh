the total time requirement of the algorithm is only

$O(\sqrt{n}\log^3 n).$

Furthermore, this is a completely no-memory algorithm, with a storage requirement as low as $O(1)$ numbers.

As a matter of fact, the above no-memory "isPrime" function can also be used to solve the original problem of finding all the prime numbers between 2 and $N$. This can be done by simply scanning all the numbers from 2 to $N$ and checking which of them is prime. Clearly, this is a completely no-memory algorithm, with storage requirement as low as $O(1)$ numbers. (The prime numbers found throughout the algorithm can be immediately printed onto some external file for safekeeping.) Furthermore, its time requirement is of order

$\frac{1}{2}\int_{2}^{N} \sqrt{x}\log^2 x\,dx = \frac{1}{2}\cdot\frac{2}{3}\left(x^{3/2}\log^2 x - \frac{4}{3}\left(x^{3/2}\log x - \frac{2}{3}x^{3/2}\right)\right)\Bigg|_{2}^{N}$

$\sim \frac{1}{3}N^{3/2}\log^2 N.$

This time requirement is only slightly larger than that in Section 5.16.

# 5.21 Coprime

Let us now introduce an algorithm to find a coprime of a given number $n$, that is, a number that shares no common divisor with $n$. For this purpose, let us first implement Euclid’s algorithm to find the greatest common divisor of two given numbers $m > n$ (see the exercises at the end of Chapter 1):

```
template<class T>
const T GCD(const T& m, const T& n) {
    T mModn = m;
    return (mModn%n) >= 1 ? GCD(n,mModn) : n;
} // greatest common divisor
```

We can now simply iterate in a loop until a coprime of the given number `n` is reached:

```
template<class T>
const T
coprime(const T&n){
    for(T co = 5; ; ++co)
        if(GCD(n,co) == 1)
            return co;
} // coprime
```

The advantage of this implementation is that the resulting coprime is rather small. This turns out to be an advantage in applications in cryptography, as discussed below.