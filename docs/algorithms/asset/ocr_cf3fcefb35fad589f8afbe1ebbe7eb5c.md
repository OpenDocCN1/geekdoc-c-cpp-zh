# 34

# 1.4 Cryptography

Proof. If the mapping $x \mapsto x^e \bmod N$ is invertible, it must be a bijection; hence statement 2 implies statement 1. To prove 2, we start by observing that $e$ is invertible modulo $(p-1)(q-1)$ which is relatively prime to this number. To see that $(x^e)^d \equiv x \bmod N$, we amplify the exponent: since $ed \equiv 1 \bmod{(p-1)(q-1)}$, we can write $ed$ in the form $1+k(p-1)(q-1)$ for some $k$. Now we need to show that difference

```
$x^{ed} - x = x^{1+k(p-1)(q-1)} - x$
```

is always 0 modulo $N$. The second method of checking is convenient because it can be simplified using Fermat's little theorem. $x^{p-1} \equiv 1 \bmod p$ and likewise by $q$. Since $p$ and $q$ are primes, this expression must also be divisible by their product $N$. Hence $x^{ed}-x = x^{1+k(p-1)(q-1)}-x \equiv 0 \(bmod N)$, exactly as we need. ■

**Figure 1.9** RSA.

Bob chooses his public and secret keys.

+   * He starts picking two large (n-bit) random primes $p$ and $q$.\n* His public key $(N, e)$ where $N=pq$ and $e$ is a $2n$-bit number relatively prime to $(p-1)(q-1)$. A common choice is $e=3$ because it permits fast encoding.\n* His secret key $d$, the inverse of $e$ modulo $(p-1)(q-1)$, computed using the extended Euclid algorithm.

Alice wishes to send message $x$ to Bob.

+   * She looks up his public key $(N, e)$ and sends her $y = (x^e \bmod N)$, computed using an efficient modular exponentiation algorithm.\n* He decodes the message by computing $y^d \bmod N$.

The RSA protocol is summarized in Figure 1.9. It is certainly convenient: the computations it requires of Alice and Bob. But how is it secure against Eve?

The security of RSA hinges on a simple assumption:

> Given $N, e$, and $y = x^e \bmod N$, it is computationally intractable to determine $x$.

This assumption is plausible. How might Eve try to guess $x$? She could experiment with all possible values of $x$, each checking whether $x^e \equiv y \bmod N$, but this would take exponential time. Or she could try to factor $N$ to retrieve $p$ and $q$, and then figure out $d$ by inverting $e$ modulo $(p-1)(q-1)$, but we believe factoring to be hard. Intractability is normally a source of dismay; the insight of RSA lies in using it to its advantage.