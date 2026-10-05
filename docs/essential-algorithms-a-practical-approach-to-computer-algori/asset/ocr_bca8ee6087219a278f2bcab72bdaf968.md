# 416 Chapter 16 = Cryptography

you sign it. Later, someone else can examine the document to verify that you have signed it. If someone modifies the document, that person cannot sign it in your name.

Typically a digital signature system includes three parts:

+   - A key-generation algorithm that creates private and public keys
- A signing algorithm that uses the private key to sign a document
- A verification algorithm that uses a public key that you publish to verify that you did sign the document

In a sense, a digital signature is the opposite of a private-key encryption system. In a private-key encryption system, any number of senders can use a public key to encrypt a message, and a single receiver uses a private key to decrypt the message. In a digital signature, a single sender uses a private key to sign a message, and then any number of receivers can use a public key to verify the signature.

# Summary

This chapter explained a few cryptographic algorithms. The simpler forms, such as transposition and substitution ciphers, are not cryptographically secure, but they provide some interesting exercises. Any student of algorithms should also have experience with these, particularly Caesar and Vigenère ciphers.

The algorithms described later in the chapter explained how many of the current-of-the-art algorithmic work AES, which uses substitution-permutation networks, and RSA, which uses public-key encryption, are two of the most used algorithms today. Although DES is no longer considered completely secure, it uses a Feistel cipher, which is still interesting and can produce secure encryption schemes such as triple DES.

This chapter covered only a tiny percentage of the cryptographic algorithms that have been studied. For more information, search online or search a book on cryptography. Two places you can start your search online include http://en.wikipedia.org/wiki/Cryptography and http://mathworld.wolfram.com/Cryptography.html. If you prefer a book, I highly recommend Applied Cryptography: Protocols, Algorithms, and Source Code in C, Second Edition by Bruce Schneier (Wiley, 1996). It describes a huge number of algorithms for encryption and decryption, digital signatures, authentication, secure elections, and digital money.

All of these algorithms rely on the fact that you can perform some calculations relatively easily if you know the key and an attacker cannot perform the same operation without knowing the key. For example, in RSA the receiver can easily decrypt messages, but an attacker cannot without factoring the product