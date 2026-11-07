# RSA Algorithm Step 4—Select the Public-Key Exponent (e) for Encryption Calculations

Next, we choose an exponent, e, for encryption, which is subject to the following rules:

+   - 1 < e < Φ(n)
+   - e must be coprime with Φ(n).

Two integers are coprime if they have no common factors other than 1.

In our example, the integers that satisfy the first rule for Φ(n) = 192 are the values 2–191. The prime factorization of 192 is

```
192 = 2 * 2 * 2 * 2 * 2 * 2 * 2 * 3
```

The value for e must be coprime with Φ(n), so we must eliminate from consideration for e any prime factors and all their multiples. Thus, the value 2 and all the other even integers from 2–190 are eliminated, as are the value 3 and all its multiples. This leaves the following odd values as possible values for e:

5 7 11 13 17 19 23 25 29 31 35 37 41 43 47 49
53 55 59 61 65 67 71 73 77 79 83 85 89 91 95 97
101 103 107 109 113 115 119 121 125 127 131 133 137 139 143 145
149 151 155 157 161 163 167 169 173 175 179 181 185 187 191

Any of these values can be used as the public encryption key's exponent (e). For our continuing discussion we'll choose 37, so our public key is (37, 221).

# RSA Algorithm Step 5—Select the Private-Key Exponent (d) for Encryption Calculations

The final step is to determine the private key's exponent, d, for decryption. We must choose a value for d such that

```
(d * e) mod Φ(n) = 1
```

In our example, the first value of d for which this is true is 109. We can check whether the preceding calculation produces 1 by plugging in the values of d, e and Φ(n):

```
(109 * 37) mod 192
```

The value of 109 * 37 is 4033. If you multiply 192 by 21, the result is 4032, leaving a remainder of 1. So, 109 is a valid value for d. There are many potential values of d—each is 109 plus a multiple of the totient (192). For instance, 301 (109 + 1 * 192):

```
(301 * 37) mod 192
```

301 * 37 is 11137, which has the remainder 1 when divided by 192—192 * 58 is 11136, leaving a remainder of 1. So values for d such as the following will work:

109 301 493 685 877 ...

We chose 109, so our private key is (109, 221).

# Encrypting a Message with RSA

Once you have the public key, it's easy to encrypt a message using RSA. Given a plaintext integer message (M) to encrypt into ciphertext (C) and a public key consist-