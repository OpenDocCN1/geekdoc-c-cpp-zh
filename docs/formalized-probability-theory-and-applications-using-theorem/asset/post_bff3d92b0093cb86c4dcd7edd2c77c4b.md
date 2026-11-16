
returns a list of digits. The decoder performs the inverse operations to convert a list of digits back to a string. The functions encode and decode have the following HOL4 types:

```
|- encode: string -> num list
|- decode: num list -> string
```

### 11.3.2 Encryption-Decryption

The encryption and decryption blocks are formalized as two functions, encrypt and decrypt, taking as input a pair of same length lists of digits and returning a list of digits.

```
|- encrypt: (num list, num list) -> num list
|- decrypt: (num list, num list) -> num list
```

The encryption is performed by a modulo 10 addition, digit by digit, of the list representing the encoded message and the list of digits representing the one-time pad key. The result of this operation is a cipher text, which is also represented by a list of digits. On the receiver side, the cipher text is decrypted by subtracting, modulo 10, the key from cipher text, resulting into a list of numbers that represent the original message. In the case where the plaintext is encoded into bits instead of digits, both encryption and decryption are performed by a simple XOR operation. We formalize encrypt in higher-order logic, recursive. h1 and h2 represent the first elements or heads of the lists l1 and l2 and their tails. The :: operator is the list constructor.

```
|- encrypt ([] , []) = [] /\ ∀ t1 t2 h1 h2.
encrypt (h1:: t1, h2:: t2) =
(h1 + h2) MOD 10:: encrypt (t1, t2)
```

Similarly, we formalize the decryption block as follows.

```
|- decrypt ([] , []) = [] /\ ∀ t1 t2 h1 h2.
decrypt (h1:: t1, h2:: t2) =
(h1 - h2) MOD 10:: decrypt (t1, t2)
```

Finally, let m be the original message (plaintext), k be the one-time pad key and r be the received message after decryption and decoding. The one-time pad (OTP) encryption is then formalized in HOL4 using the following predicate.

```
|- ∀ m k r.
   OTP m k r <=>
   r = decode (decrypt (encrypt (encode m, k), k))
```

As a reassuring property, we prove in HOL4 that the one-time pad as designed and formalized above, ensures that the received message is equal to the original message.

```
|- ∀ m k r. OTP m k r => (r = m)
```

### 11.3.3 Perfect Security

We formally verify that the one-time pad provides perfect security by proving that the information leakage degree, formalized in Chapter 4 Section 4.3, is equal to one. Let M,C and K denote the random variables representing the plaintext, ciphertext and keys, respectively. Hence, K is uniformly distributed and is independent of M, which allows us to prove that

```
|- ∀ m ∈ M, c ∈ C.
   P (M = m | C = c) = P (M = m)
```

This follows from the following lemmas, which we prove using the properties we formally proved in Chapter 4 about probability distributions.

- |- P (M = m | C = c) = P (M = m, C = c) / P (C = c)
- |- P (M = m, C = c) = P (M = m, K = m ⊕ c)
- |- P (M = m, K = m ⊕ c) = P (M = m) P (K = m ⊕ c)
- |- P (K = m ⊕ c) = 2^-n
- |- P (C = c) = 2^-n

Next, we prove that the conditional entropy of M given C is equal to the entropy of M and that the mutual information I (M; C) is equal to zero.

- |- H (M | C) = H (M)
- |- I (M; C) = 0

Finally, it follows that the information leakage degree is equal to 1, meaning that the one-time pad encryption is information-theoretically secure and there is no leakage of information about the secret input (plaintext) to a possible eavesdropper.

```
H D (M, C) = 1
```

In this application, we were able to formally prove the perfect security property of the OTP encryption system thanks to the various properties of probability distributions presented in Section 4.1 of Chapter 4 as well as the properties of the Shannon entropy and mutual information from Section 4.2 of the same Chapter. Theorem proving allows to provide a generic result that does not depend on which message has been encrypted, unlike the kind of results produced by computer simulation. In fact, simulation can be used to detect the presence of bugs but is not useful to guarantee their absence. The formalization of the different components of the OTP as well as the proof of its security property required around two weeks of human effort and around 800 lines of code.

### 11.4 CONCLUSION

In this chapter, we have verified some classical results of probability theory, namely, the Chebyshev and Markov inequalities and the Weak Law of Large Numbers. We used these results to formally verify the Asymptotic Equipartition Property, an important property used in the proofs of numerous information-theoretic theorems. We used the AEP to verify the properties of a typical encoder that is used in the formal proof of the Shannon source coding theorem. We have also presented two example applications of the use of quantitative analysis within a theorem prover to analyse the properties of an anonymity-based MIX channel as well as the properties of the one-time pad encryption. In the first example, we were able to detect a problem and come up with a counter-example to a result that was reported in a prominent paper by Zhu and Bettati. In the second example, we were able to formalize the encryption system, verify its functionality as well as to prove a generic result about its perfect security. The soundness and the deduction style of the theorem prover guaranteed the validity of the analysis when deriving these proofs. Besides, the results of this type of analysis are generic and valid for any instance of the system. We argue that these benefits are even more significant when dealing with larger and more complex systems as is the case for nowadays parallel and distributed systems. These applications illustrate how our formalization of information theory and the different underlying theories of measure, Lebesgue integration and probability, can be used to reason about a multitude of engineering applications. Conducting the analysis within the sound core of a theorem prover helped to add more trust to the proved results. It allowed detecting a bug in the paper-and-pencil analysis of the MIX channel example.

## REFERENCES

- Affeldt, R., & Hagiwara, M. (2012). Formalization of Shannon's theorems in SSReflect-Coq. In I. T. Proving (Ed.), LNCS (Vol. 7406, pp. 233–249). Springer. doi:10.1007/978-3-642-32347-8_16
- Chaum, D. L. (1981). Untraceable electronic mail, return addresses, and digital pseudonyms. Communications of the ACM, 24(2), 84–90. doi:10.1145/358549.358563
- Cover, T. M., & Thomas, J. A. (1991). Elements of information theory. Wiley-Interscience. doi:10.1002/0471200611
- Gallager, R. G. (1968). Information theory and reliable communication. John Wiley & Sons, Inc.
- Gray, R. M. (1990). Entropy and information theory. Springer-Verlag. doi:10.1007/978-1-4757-3982-4
- Reiter, M. K., & Rubin, A.D. (1998). Crowds: Anonymity for web transactions. ACM Transactions on Information Systems Security, 1(1), 66–92.
- Syverson, P. F., & Goldschlag, D. M. (1997). Anonymous connections and onion routing. In Proceedings of Symposium on Security and Privacy (pp. 44–54). IEEE Computer Society.
- Zhu, Y., & Bettati, R. (2009). Information leakage as a model for quality of anonymity networks. IEEE Transactions on Parallel and Distributed Systems, 20(4), 540–552. doi:10.1109/TPDS.2008.100

## KEY TERMS AND DEFINITIONS

**Asymptotic Equipartition Property:** Asymptotic equipartition property (AEP) is the foundational property behind the concept of a typical set and allows us to acquire the output samples of a stochastic process.

**Data Compression:** Data compression involves encoding information using fewer bits than the original representation. Data compression may or may not lead to data losses.

**Pseudorandom Number Generation and a Typical Set:** A pseudorandom number whose output sequence lies outside the typical set by some statistical standards is rejected as insufficiently random.

## Chapter 12
Reliability Theory

## ABSTRACT

In this chapter, some basic concepts of reliability theory, namely cumulative distribution function, survival function and hazard function, and reliability block diagrams, are described and their higher-order-logic formalization is presented. Some of the important properties of these reliability concepts are formally verified using the HOL4 theorem prover to facilitate reasoning about reliability of engineering systems.
