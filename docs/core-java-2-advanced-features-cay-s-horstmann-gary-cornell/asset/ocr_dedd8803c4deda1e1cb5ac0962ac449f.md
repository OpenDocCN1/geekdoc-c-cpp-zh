It then produces a file that contains

+   - The length of the wrapped key
+   - The wrapped key bytes
+   - The plaintext encrypted with the AES key

The `-decrypt` option decrypts such a file. To try the program, first generate the RSA keys:

```
java rsa.RSATest -genkey public.key private.key
```

Then encrypt a file:

```
java rsa.RSATest -encrypt plaintextFile encryptedFile public.key
```

Finally, decrypt it and verify that the decrypted file matches the plaintext:

```
java rsa.RSATest -decrypt encryptedFile decryptedFile private.key
```

# **Listing 9.20** `rsa/RSATest.java`

```
```java
package rsa;

import java.io.*;
import java.security.*;
import javax.crypto.*;

/**
 * This program tests the RSA cipher. Usage:<br>
 * java rsa.RSATest -genkey public private<br>
 * java rsa.RSATest -encrypt plaintext encrypted public<br>
 * java rsa.RSATest -decrypt encrypted decrypted private<br>
 * @author Cay Horstmann
 * @version 1.01 2012-06-10
 */
public class RSATest
{
   private static final int KEYSIZE = 512;

   public static void main(String[] args)
      throws IOException, GeneralSecurityException, ClassNotFoundException
   {
      if (args[0].equals("-genkey"))
      {
         KeyPairGenerator pairgen = KeyPairGenerator.getInstance("RSA");
         SecureRandom random = new SecureRandom();
         pairgen.initialize(KEYSIZE, random);
         KeyPair keyPair = pairgen.generateKeyPair();
```
```

_(Continues)_