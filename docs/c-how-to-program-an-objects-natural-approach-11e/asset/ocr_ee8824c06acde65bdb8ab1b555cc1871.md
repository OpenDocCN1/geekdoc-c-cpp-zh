# Cryptography

Cryptography has been used for thousands of years⁽²⁷,²⁸⁾ and is critically important in today’s connected world. Every day, cryptography is used behind the scenes to ensure that your Internet-based communications are private and secure. For example, most websites now use the HTTPS protocol to encrypt and decrypt your web interactions, as we do at `deitel.com`.

# Caesar Cipher

Julius Caesar used a simple substitution cipher to encrypt military communications.⁽²⁹⁾ His technique—known as the Caesar cipher⁽³⁰⁾—replaces every letter in a communication with the letter three ahead in the alphabet. So, A is replaced with D, B with E, C with F, … X with A, Y with B and Z with C. Thus, the plaintext

```
Caesar Cipher
```

would be encrypted as

```
Fdhvdu Flskhu
```

The encrypted text is known as the ciphertext.

# Vigenère Cipher

Simple substitution ciphers like the Caesar cipher are relatively easy to decrypt. For example, the letter “e” is the most frequently used letter in English. So, you could study ciphertext encrypted with the Caesar cipher and assume with a high likelihood that the character appearing most frequently is probably an “e.”

In this example, you’ll use a Vigenère cipher, which is a secret-key substitution cipher. This cipher is implemented using 26 Caesar ciphers—one for each letter of the alphabet. A Vigenère cipher uses letters from the plaintext and secret key to look up replacement characters in the various Caesar ciphers.⁽³¹⁾

For this cipher, the secret key must be composed of letters. Like passwords, the secret key should not be easy to guess. We used the 11 randomly selected characters

```
XMWUJBVYHXZ
```

There’s no limit to the number of characters you can use in your secret key. However, the person decrypting the ciphertext must know the secret key originally used to create the ciphertext. Presumably, you’d provide that in advance—possibly in a face-to-face meeting.

# Using Our Cipher Class

For the example in Fig. 5.18, you’ll use our class `Cipher`, which implements the Vigenère cipher. The header `"cipher.h"` (line 3) from the ch05 examples folder defines the class.

+   27. “Cryptography.” Wikipedia. Wikimedia Foundation. Accessed April 14, 2023. https://en.wikipedia.org/wiki/Cryptography#History_of_cryptography_and_cryptanalysis.
+   28. Binance Academy. “History of Cryptography.” Updated December 23, 2022. Accessed April 14, 2023. https://www.binance.vision/security/history-of-cryptography.
+   29. “Caesar Cipher.” Wikipedia. Wikimedia Foundation. Accessed April 14, 2023. https://en.wikipedia.org/wiki/Caesar_cipher.
+   30. For a fun way to play with the Caesar cipher and many other cipher techniques, check out the website https://cryptii.com/pipes/caesar-cipher, which is an online implementation of the open-source cryptii project: https://github.com/cryptii/cryptii.
+   31. See https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher to learn about the implementation.