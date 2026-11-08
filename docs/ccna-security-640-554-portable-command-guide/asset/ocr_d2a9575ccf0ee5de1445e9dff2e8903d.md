**NOTE:** Notice the comparatively short symmetric key lengths. However, do not directly compare the key length of asymmetric and symmetric algorithms; the underlying design of the two algorithm families differs greatly.

**NOTE:** An 80-bit symmetric key is considered equal to a 1024-bit key using the RSA algorithm. A 112-bit symmetric key is considered equal to a 2048-bit key using the RSA algorithm. A 128-bit symmetric key is considered equal to a 3072-bit key using the RSA algorithm.

# Cryptographic Hashes

Cryptographic hashes are based on one-way functions that are used for integrity assurance. They hash arbitrary data into a fixed-length digest known as a fingerprint.

**NOTE:** Hashing alone does not add security to the message. It only prevents the message from being changed accidentally, such as by a communication error.

# Well-Known Hashing Algorithms

| Algorithm | Description |
|---|---|
| **Message digest algorithm 5 (MD5)** | Popular, ubiquitous hashing algorithm<br>Collision-resistant one-way function, which means that two messages with the same hash are very unlikely to occur<br>128-bit message digest |
| **Secure Hash Algorithm 1 (SHA-1)** | Although slower than MD5, it is the stronger algorithm.<br>160-bit message digest |
| **Secure Hash Algorithm 2 (SHA-2)** | Available as SHA-224, SHA-256, SHA-384, and SHA-512<br>Should be used rather than SHA-1<br>Adopted by U.S. federal government as a secure hash standard |

# Hash-Based Message Authentication Codes

Hash-based Message Authentication Codes (HMAC) use existing hash functions and add a secret key as input to the hash function to provide integrity assurance and authentication. Only parties who have access to that secret key can compute the digest of an HMAC function.

**NOTE:** HMACs defeat man-in-the-middle attacks.