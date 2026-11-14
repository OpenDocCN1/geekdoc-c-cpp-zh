![](bbox=[0.26, 0.08, 0.74, 0.43])

# Figure 8.4.3 Basic Encryption/Decryption Schemes.

hash message digest checksum digital fingerprint Non-key algorithms, also known as hash, message digest, checksum, or digital fingerprint, employ a hashing function or algorithm that takes an arbitrary string (the message) as input and produces a fixed length string as output. With such a scheme, two different messages being hashed to the same value should be impossible. Thus, if the receiver hashes a received message and the result of the hash is a different value from the intended, the receiver can know that the message has been tampered with.

MD5 algorithm The MD5 algorithm, which produces a 128-bit hash value, is an example of such a hash function. However, while still in use, like the DES algorithm, MD5 has been designated as essentially broken.

Public key algorithms are supported by two keys: one public and one private. A message is encrypted using the public key and decrypted using the private. RSA is an example of such an algorithm. The encryption utilizes a public key and the decryption utilizes a private key. The keys are 512 bits long and are computed based upon very large prime numbers.

+   Key Management and Agreement

Secure Operations Center (SOC) TrustZone key-agreement protocol The secure key(s) must be kept inside of a secure device that is itself protected by a combination of hardware and software systems that must be able to subvert any unauthorized access attempts. Such a device is often referred to as a Secure Operations Center (SOC) or TrustZone.

If a large number of embedded systems must be dealt with, managing secret keys for all can become a challenge. A mechanism to aide in supporting the task is known as the key-agreement protocol. The protocol allows multiple parties to agree on a key such that each can affect the outcome. An important aspect of such protocols is that they do not reveal to any covertly listening individuals what key has been agreed upon.