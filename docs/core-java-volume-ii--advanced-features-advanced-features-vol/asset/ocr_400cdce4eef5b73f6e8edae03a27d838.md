If you don’t seed the random number generator, it will compute its own 20-byte seed by launching threads, putting them to sleep, and measuring the exact time when they are awakened.

> **NOTE:** This algorithm is *not* known to be safe. In the past, algorithms that relied on the timing of some components of the computer, such as hard disk access time, were shown not to be completely random.

The sample program at the end of this section puts the AES cipher to work (see Listing 10.17). The crypt utility method in Listing 10.18 will be reused in other examples. To use the program, you first need to generate a secret key. Run

```
java aes.AESTest -genkey secret.key
```

The secret key is saved in the file secret.key.

Now you can encrypt with the command

```
java aes.AESTest -encrypt plaintextFile encryptedFile secret.key
```

Decrypt with the command

```
java aes.AESTest -decrypt encryptedFile decryptedFile secret.key
```

The program is straightforward. The -genkey option produces a new secret key and serializes it in the given file. That operation takes a long time because the initialization of the secure random generator is time-consuming. The -encrypt and -decrypt options both call into the same crypt method that calls the update and doFinal methods of the cipher. Note how the update method is called so long as the input blocks have the full length, and the doFinal method is either called with a partial input block (which is then padded) or with no additional data (to generate one pad block).

```
Listing 10.17  aes/AESTest.java

1  package aes;
2
3  import java.io.*;
4  import java.security.*;
5  import javax.crypto.*;
6
```