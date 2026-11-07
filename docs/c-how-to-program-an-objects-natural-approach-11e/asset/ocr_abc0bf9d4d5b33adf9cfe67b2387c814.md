# RSA Algorithm Step 3—Calculate the Totient Function

Calculate Φ(n)—pronounced “phi of n”—which is Euler’s totient function.⁶³ This is calculated simply as:

Φ(n) = (p − 1) * (q − 1)

Given p = 13 and q = 17, Φ(n) is

Φ(n) = 12 * 16 = 192

This number is used in the calculations that determine the **encryption exponent (e)** and **decryption exponent (d)**, which will help us encrypt plaintext and decrypt ciphertext, respectively, as you’ll see below.

# RSA Algorithm Step 4—Select the Public-Key Exponent (e) for Encryption Calculations

Next, we choose an exponent, **e, for encryption**, which is subject to the following rules:

+   - 1 < e < Φ(n)
+   - e must be coprime with Φ(n).

Two integers are coprime if they have no common factors other than 1.
In our example, the integers that satisfy the first rule for Φ(n) = 192 are the values 2–191. The prime factorization of 192 is

192 = 2 * 2 * 2 * 2 * 2 * 2 * 3

The value for e must be coprime with Φ(n), so we must eliminate from consideration for e any prime factors and all their multiples. Thus, the value 2 and all the other even integers from 2–190 are eliminated, as are the value 3 and all its multiples. This leaves the following odd values as possible values for e:

+   5 7 11 13 17 19 23 25 29 31 35 37 41 43 47 49
+   53 55 59 61 65 67 71 73 77 79 83 85 89 91 95 97
+   101 103 107 109 113 115 119 121 125 127 131 133 137 139 143 145
+   149 151 155 157 161 163 167 169 173 175 179 181 185 187 191

Any of these values can be used as the public encryption key’s exponent (e). For our continuing discussion we’ll choose 37, so **our public key is (37, 221).**

# RSA Algorithm Step 5—Select the Private-Key Exponent (d) for Encryption Calculations

The final step is to **determine the private key’s exponent, d, for decryption.** We must choose a value for d such that

(d * e) mod Φ(n) = 1

In our example, the first value of d for which this is true is 109. We can check whether the preceding calculation produces 1 by plugging in the values of d, e and Φ(n):

(109 * 37) mod 192

⁶³ “Euler’s totient function.” Accessed April 14, 2023. https://en.wikipedia.org/wiki/Euler%27s_totient_function.