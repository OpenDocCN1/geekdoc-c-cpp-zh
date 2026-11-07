# RSA Algorithm Steps

Steps 1–5 below use small integer values to explain how the RSA algorithm generates a public-key/private-key pair. Then, Step 6 uses the public key to encrypt plaintext into ciphertext, and Step 7 uses the private key to decrypt the ciphertext back to the original plaintext. The steps we show are based on the original RSA paper and the RSA Algorithm Wikipedia page.

# RSA Algorithm Step 1—Choose Two Prime Numbers

Choose two different prime numbers p and q. For this case study, we’ll use small prime numbers—p = 13 and q = 17. This will keep the calculations manageable in our discussions and on your computer using C with its limited-range, built-in integer data types. In commercial-grade RSA cryptography systems, these prime numbers typically are hundreds of digits each and chosen at random. For a sense of how large the integers in RSA can be, visit the RSA Numbers webpage

https://en.wikipedia.org/wiki/RSA_numbers

which shows various integers from 100 to 617 digits in length. The C integer data types int, long int and long long int cannot hold integers this large, so special processing is required to accommodate such large numbers.

# RSA Algorithm Step 2—Calculate the Modulus (n), Which Is Part of Both the Public and Private Keys

Calculate the modulus n, which is simply the product of p and q:

```
n = p * q
```

Based on p = 13 and q = 17, n is 221. As you’ll see, n is part of both the public and private keys. The p and q values are kept private.

# RSA Algorithm Step 3—Calculate the Totient Function

Calculate Φ(n)—pronounced “phi of n”—which is Euler’s totient function. This is calculated simply as:

```
Φ(n) = (p - 1) * (q - 1)
```

Given p = 13 and q = 17, Φ(n) is

```
Φ(n) = 12 * 16 = 192
```

This number is used in the calculations that determine the encryption exponent (e) and decryption exponent (d), which will help us encrypt plaintext and decrypt ciphertext, respectively, as you’ll see below.