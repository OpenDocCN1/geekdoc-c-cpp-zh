
data has fewer than eight bytes. Of course, we can fill the remaining bytes with 0, to obtain one final block of eight bytes, and encrypt it. But when the blocks are decrypted, the result will have several trailing 0 bytes appended to it, and therefore will be slightly different from the original input file. To avoid this problem, we need a *padding scheme*. A commonly used padding scheme is the one described in the Public Key Cryptography Standard (PKCS) #5 by RSA Security, Inc. (https://tools.ietf.org/html/rfc2898).

In this scheme, the last block is not padded with a pad value of zero, but with a pad value that equals the number of pad bytes. In other words, if L is the last (incomplete) block, it is padded as follows:

```
L 01                         if length(L) = 7
L 02 02                      if length(L) = 6
L 03 03 03                   if length(L) = 5
. . . .
L 07 07 07 07 07 07 07      if length(L) = 1
```

Finally, if the length of the input is actually divisible by 8, then one block

```
08 08 08 08 08 08 08 08
```

is appended to the input and encrypted. After decryption, the very last byte of the plaintext is a count of the padding characters to discard.

## 9.5.2 Key Generation

To encrypt, you need to generate a key. Each cipher has a different format for keys, and you need to make sure that the key generation is random. Follow these steps:

- 1. Get a `KeyGenerator` for your algorithm.
- 2. Initialize the generator with a source for randomness. If the block length of the cipher is variable, also specify the desired block length.
- 3. Call the `generateKey` method.

For example, here is how you generate an AES key:

```java
KeyGenerator keygen = KeyGenerator.getInstance("AES");
SecureRandom random = new SecureRandom(); // see below
keygen.init(random);
Key key = keygen.generateKey();
```

Alternatively, you can produce a key from a fixed set of raw data (perhaps derived from a password or the timing of keystrokes). Construct a `SecretKeySpec` (which implements the `SecretKey` interface) like this:

```java
byte[] keyData = ...; // 16 bytes for AES
SecretKey key = new SecretKeySpec(keyData, "AES");
```

When generating keys, make sure you use *truly random* numbers. For example, the regular random number generator in the `Random` class, used by the current date and time, is not random enough. Suppose the computer clock is accurate to 1/10 of a second. Then there are at most 864,000 seeds per day. If an attacker knows the day a key was issued (which can often be deduced from a message date or certificate expiration date), it is an easy matter to generate all possible seeds for that day.

The `SecureRandom` class generates random numbers that are far more secure than those produced by the `Random` class. You still need to provide a seed to start the number sequence at a random spot. The best method for doing this is to obtain random input from a hardware device such as a white-noise generator. Another reasonable source for random input is to ask the user to type away aimlessly on the keyboard, with each keystroke contributing only one or two bits to the random seed. Once you gather such random bits in an array of bytes, pass it to the `setSeed` method:

```java
SecureRandom serand = new SecureRandom();
byte[] b = new byte[20];
// fill with truly random bits
serand.setSeed(b);
```

If you don’t seed the random number generator, it will compute its own 20-byte seed by launching threads, putting them to sleep, and measuring the exact time when they are awakened.

> **NOTE:** This algorithm is *not* known to be safe. In the past, algorithms that relied on the timing of some components of the computer, such as hard disk access time, were shown not to be completely random.

The sample program at the end of this section puts the AES cipher to work (see Listing 9.18). The crypt utility method in Listing 9.19 will be reused in other examples. To use the program, you first need to generate a secret key. Run

```bash
java aes.AESTest -genkey secret.key
```

The secret key is saved in the file `secret.key`.

Now you can encrypt with the command

```bash
java aes.AESTest -encrypt plaintextFile encryptedFile secret.key
```

Decrypt with the command

```bash
java aes.AESTest -decrypt encryptedFile decryptedFile secret.key
```

The program is straightforward. The -genkey option produces a new secret key and serializes it in the given file. That operation takes a long time because the initialization of the secure random generator is time-consuming. The -encrypt and -decrypt options both call into the same crypt method that calls the update and doFinal methods of the cipher. Note how the update method is called as long as the input blocks have the full length, and the doFinal method is either called with a partial input block (which is then padded) or with no additional data (to generate one pad block).

### Listing 9.18 `aes/AESTest.java`

```java
package aes;

import java.io.*;
import java.security.*;
import javax.crypto.*;

/**
 * This program tests the AES cipher. Usage:<br>
 * java aes.AESTest -genkey keyfile<br>
 * java aes.AESTest -encrypt plaintext encrypted keyfile<br>
 * java aes.AESTest -decrypt encrypted decrypted keyfile<br>
 * @author Cay Horstmann
 * @version 1.01 2012-06-10
 */
public class AESTest
{
   public static void main(String[] args)
      throws IOException, GeneralSecurityException, ClassNotFoundException
   {
      if (args[0].equals("-genkey"))
      {
         KeyGenerator keygen = KeyGenerator.getInstance("AES");
         SecureRandom random = new SecureRandom();
         keygen.init(random);
         SecretKey key = keygen.generateKey();
         try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream(args[1])))
         {
            out.writeObject(key);
         }
      }
      else
      {
         int mode;
         if (args[0].equals("-encrypt")) mode = Cipher.ENCRYPT_MODE;
         else mode = Cipher.DECRYPT_MODE;

         try (ObjectInputStream keyIn = new ObjectInputStream(new FileInputStream(args[3]));
              InputStream in = new FileInputStream(args[1]);
              OutputStream out = new FileOutputStream(args[2]))
         {
            Key key = (Key) keyIn.readObject();
            Cipher cipher = Cipher.getInstance("AES");
            cipher.init(mode, key);
            Util.crypt(in, out, cipher);
         }
      }
   }
}
```

### Listing 9.19 `aes/Util.java`

```java
package aes;

import java.io.*;
import java.security.*;
import javax.crypto.*;

public class Util
{
    /**
     * Uses a cipher to transform the bytes in an input stream and sends the transformed bytes to
     * an output stream.
     * @param in the input stream
     * @param out the output stream
     * @param cipher the cipher that transforms the bytes
     */
    public static void crypt(InputStream in, OutputStream out, Cipher cipher)
        throws IOException, GeneralSecurityException
    {
        int blockSize = cipher.getBlockSize();
        int outputSize = cipher.getOutputSize(blockSize);
        byte[] inBytes = new byte[blockSize];
        byte[] outBytes = new byte[outputSize];

        int inLength = 0;
        boolean more = true;
        while (more)
        {
```

| `javax.crypto.KeyGenerator` | `1.4` |
|---|---|
| • `static KeyGenerator getInstance(String algorithmName)`<br>returns a KeyGenerator object that implements the specified algorithm. Throws a `NoSuchAlgorithmException` if the algorithm is not provided.<br><br>• `void init(SecureRandom random)`<br>• `void init(int keySize, SecureRandom random)`<br>initializes the key generator.<br><br>• `SecretKey generateKey()`<br>generates a new key. | |

| `javax.crypto.spec.SecretKeySpec` | `1.4` |
|---|---|
| • `SecretKeySpec(byte[] key, String algorithmName)`<br>constructs a key specification. | |

## 9.5.3 Cipher Streams

The JCE library provides a convenient set of stream classes that automatically encrypt or decrypt stream data. For example, here is how you can encrypt data to a file:

```java
Cipher cipher = ... ;
cipher.init(Cipher.ENCRYPT_MODE, key);
CipherOutputStream out = new CipherOutputStream(new FileOutputStream(outputFileName), cipher);
byte[] bytes = new byte[BLOCKSIZE];
int inLength = getData(bytes); // get data from data source
while (inLength != -1)
{
    out.write(bytes, 0, inLength);
    inLength = getData(bytes); // get more data from data source
}
out.flush();
```

Similarly, you can use a CipherInputStream to read and decrypt data from a file:

```java
Cipher cipher = ... ;
cipher.init(Cipher.DECRYPT_MODE, key);
CipherInputStream in = new CipherInputStream(new FileInputStream(inputFileName), cipher);
byte[] bytes = new byte[BLOCKSIZE];
int inLength = in.read(bytes);
while (inLength != -1)
{
```
