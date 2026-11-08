# Modern Substitution Ciphers

Modern substitution ciphers are categorized by the process they follow to encrypt text:

| Type | Description |
|---|---|
| **Block ciphers** | - Referred to as “block-by-block cipher” because it operates on large blocks of digits with a fixed, unvarying transformation.<br>- Padding is used to keep the data size a multiple of the block size.<br>- The ciphertext is generally longer than the plaintext.<br>- The block size varies by algorithm. (DES has 8 bytes.)<br>- Examples: DES, 3DES, AES, Twofish. |
| **Stream ciphers** | - Referred to as “bit-by-bit cipher,” in which each plaintext digit is encrypted one at a time with the corresponding digit of the key stream, to give a digit of the cipher-text stream.<br>- Stream ciphers operate on smaller units of plaintext (bits).<br>- The size of the message does not typically change.<br>- The transformation of smaller plaintext units varies depending on encryption requirements.<br>- Examples: RC4, SEAL. |

# Encryption Algorithms

Encryption is the process of disguising a message in such a way as to hide its original contents. Plaintext (that is, the readable message) is converted to ciphertext (the unreadable, “disguised” message).

Encryption provides confidentiality because only authorized entities can read the original message.

> **NOTE:** Historically, confidentiality was provided by the secrecy of the algorithm (method) used. Secrecy in modern encryption lies in the secrecy of the key used, not in the algorithm.

Encryption can provide confidentiality at various OSI layers, such as the following:

+   - Encrypt data link layer data using proprietary link-encrypting devices.
+   - Encrypt network layer data using protocols such as those in the IPsec protocol suite.
+   - Encrypt session layer data using protocols such as SSL or Transport Layer Security (TLS).
+   - Encrypt application layer data, such as secure email, secure database sessions (Oracle SQL*Net), and secure messaging (Lotus Notes sessions).