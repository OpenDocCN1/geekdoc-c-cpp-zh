# Chapter 16 = Cryptography 415

To save time, some cryptographic systems use public-key encryption to allow a sender and receiver to exchange a private key for use with symmetric-key encryption.

> NOTE The program Pretty Good Privacy (PGP) uses public-key encryption for at least part of its computation. To get a good level of obscurity in the ciphertext, a reasonable message length, and acceptable speed, PGP actually processes messages with a series of operations, including hashing, compression, public-key encryption, and private-key encryption.
For more information on PGP, see http://en.wikipedia.org/wiki/Pretty_good_privacy.

# Other Uses for Cryptography

The algorithms described in this chapter focus on encrypting and decrypting messages, but cryptography has other uses as well.

For example, a cryptographic hash function takes as an input block of data such as a file and returns a hash value that identifies the data. You can then make the file and hash value available publicly.

A receiver who wants to use the file can perform the same hashing function to see if the new hash value matches the published one. If someone has tampered with the file, the hash values should not match, and the receiver knows that the file is not in its original form.

A good hash function should have the following properties:

+   - It should be easy to compute.
- It should be prohibitively difficult for an attacker to create a file with a given hash value (so the attacker cannot replace the true file with a fake one).
- It should be prohibitively difficult to modify the file without changing its hash value.
- It should be prohibitively difficult to find two files with the same hash value.

One application of cryptographic hashing is password verification. You create a password, and the system stores its hash value. The system doesn't store the actual password, and an attacker who breaks into the system cannot steal the password.

Later, when you want to log into the system, you enter your password again. The system hashes and verifies that the new hash value matches the one it has saved.

A digital signature is a cryptographic tool that is somewhat similar to cryptographic hashing. If you want to prove that you wrote a particular document,