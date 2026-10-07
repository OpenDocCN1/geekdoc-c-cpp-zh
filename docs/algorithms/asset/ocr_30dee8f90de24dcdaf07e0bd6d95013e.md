# Chapter 1

# Algorithms 33

The security of AES has not been rigorously established, but currently at present the general public does not know how to break the code—to recover $x$ from $c$—except using techniques that are not much better than the brute-force approach of trying all possibilities for the shared string $r$.

# 1.4.2 RSA

Unlike the previous protocols, the RSA scheme is an example of *public-key cryptography*: anybody can send a message to anybody using publicly available information, rather like addresses or phone numbers. Each person has a public key to the whole world and a secret key only to him or herself. When Alice wants to send message $x$ to Bob, she encodes $x$ using his public key. Bob decrypts it using his secret key, retrieve $x$. Eve is welcome to see all encrypted messages for Bob as she likes, but she will not be able to decode them, under certain simple assumptions.

The RSA scheme is based heavily upon number theory. Think of messages from Alice to Bob as modulo $N$; messages larger than $N$ can be broken into smaller pieces. The encryption function will then be a bijection on $\{0, 1, \dots, N-1\}$, and the decryption function will be its inverse. What values of $N$ are appropriate, and what bijection should be used?

**Property** Pick any two primes $p$ and $q$ and let $N = pq$. For any relatively prime to $(p-1)(q-1)$:

+   1. The mapping $x \mapsto x^d \mod N$ is a bijection on $\{0, 1, \dots, N-1\}$.
2. Moreover, the inverse mapping is easily revealed: let $d$ be the inverse of $e$ modulo $(p-1)(q-1)$. Then for all $x \in \{0, \dots, N-1\}$,

> $(x)^d \equiv x \mod N$

The first property tells us that the mapping $x \mapsto x^d \mod N$ is a reasonable way to encode messages $x$; no information is lost. So, if Bob publishes $(N, e)$ as his public key, everyone can use it to send him encrypted messages. The second property tells us how decryption can be achieved. Bob should retain the value $d$ as his *secret key*, with which he can decode all messages that come to him by simply raising them to the $d$th power modulo $N$.

*Example.* Let $N = 55 = 5 \cdot 11$. Choose encryption exponent $e = 3$, which satisfies the condition $gcd(e, (p-1)(q-1)) = \gcd(3, 40) = 1$. The decryption exponent is $d = 3^{-1} \mod 27$. For any message $x$ mod 55, the encryption of $x$ is $y = x^3 \mod 55$, and the decryption of $y$ is $x = y^{27} \mod 55$. So, for example, if $x = 13$, then $y = 13^3 = 52 \mod 55$ and $13 = 52^{27} \mod 55$.

Let's prove the assertion above and examine the security of the scheme.