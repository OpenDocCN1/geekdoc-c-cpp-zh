failure probability the worst-case 1/2 bound that we proved earlier. Numbers that pass this test have been Jokingly referred to as “industrial grade primes.” The resulting algorithm is quite fast, generating primes that are hundreds of bits long in a fraction of a second on a PC.

The important question remains: what is the probability that the output is really prime? To answer we must first understand how discerning the Fermat test is. As a concrete example, suppose we perform the test with base $a=2$ for all numbers $N \le 25 	imes 10^9$. In this range, there are about $10^9$ primes, and about 20,000 composites it encodes in private (see the following figure). Thus the chance of erroneously outputting a composite is approximately $20,000/10^9 = 2 	imes 10^{-5}$. This chance of error decreases rapidly as the length of the numbers involved is increased (to the few hundred digits we expect in our applications).

![](bbox=[0.047, 0.398, 0.718, 0.532])

# 1.4 Cryptography

Our next topic, the Rivest-Shamir-Adleman (RSA) cryptystem, uses all the ideas we have introduced in this chapter! It derives very strong guarantees of security by ingeniously exploiting the wide gulf between the polynomial-time computability of certain number-theoretic aspects (modular exponentiation, greatest common divisor, primality testing) and the intractability of others (factoring).

The typical setting for cryptography can be described via a cast of three characters: Alice and Bob, who wish to communicate in private, and Eve, an eavesdropper who will go to lengths to find out what they are saying. For concreteness, let's say Alice wants to send a specific message $x$, written in binary (why not), to her friend Bob. Bob encodes it $e(x)$, sends it over, and then applies his decryption function $d(\cdot)$ to decrypt it: $d(e(x))=x$. Here $e(x)$ and $d(\cdot)$ are appropriate transformations of the messages.

Alice and Bob are worried that the eavesdropper, Eve, will intercept $e(x)$: for in-stance, she might be a sniffer on the network. But ideally the encryption function