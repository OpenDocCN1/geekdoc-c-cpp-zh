
- A forger who is in possession of a given message cannot construct a fake message that has the same message digest as the original.

The second property is, again, a matter of probabilities. Consider the following message by the billionaire father:

> “Upon my death, my property shall be divided equally among my children; however, my son George shall receive nothing.”

That message (with a final newline) has an SHA-1 fingerprint of

```text
12 5F 09 03 E7 31 30 19 2E A6 E7 E4 90 43 84 B4 38 99 8F 67
```

The distrustful father has deposited the message with one attorney and the fingerprint with another. Now, suppose George bribes the lawyer holding the message. He wants to change the message so that Bill gets nothing. Of course, that changes the fingerprint to a completely different bit pattern:

```text
70 F6 AB 08 EB 40 EC CD AB 74 ED E9 86 F9 ED 99 D1 45 81 57
```

Can George find some other wording that matches the fingerprint? If he had been the proud owner of a billion computers from the time the Earth was formed, each computing a million messages a second, he would not yet have found a message he could substitute.

A number of algorithms have been designed to compute such message digests. Among them are SHA-1, the secure hash algorithm developed by the National Institute of Standards and Technology, and MD5, an algorithm invented by Ronald Rivest of MIT. Both algorithms scramble the bits of a message in ingenious ways. For details about these algorithms, see, for example, *Cryptography and Network Security, Fifth Edition*, by William Stallings (Prentice Hall, 2011). However, subtle regularities have been discovered in both algorithms, and NIST recommends to switch to stronger alternatives such as SHA-256, SHA-384, or SHA-512.

The Java programming language implements MD5, SHA-1, SHA-256, SHA-384, and SHA-512. The `MessageDigest` class is a factory for creating objects that encapsulate the fingerprinting algorithms. It has a static method, called `getInstance`, that returns an object of a class that extends the `MessageDigest` class. This means the `MessageDigest` class serves double duty:

- As a factory class
- As the superclass for all message digest algorithms

For example, here is how you obtain an object that can compute SHA fingerprints:

```java
MessageDigest alg = MessageDigest.getInstance("SHA-1");
```

(To get an object that can compute MD5, use the string "MD5" as the argument to `getInstance`.)

After you have obtained a MessageDigest object, feed it all the bytes in the message by repeatedly calling the update method. For example, the following code passes all bytes in a file to the alg object just created to do the fingerprinting:

```java
InputStream in = . . .;
int ch;
while ((ch = in.read()) != -1)
    alg.update((byte) ch);
```

Alternatively, if you have the bytes in an array, you can update the entire array at once:

```java
byte[] bytes = . . .;
alg.update(bytes);
```

When you are done, call the digest method. This method pads the input as required by the fingerprinting algorithm, does the computation, and returns the digest as an array of bytes.

```java
byte[] hash = alg.digest();
```

The program in Listing 9.16 computes a message digest, using MD5, SHA-1, SHA-256, SHA-384, or SHA-512. Run it as

```text
java hash.Digest hash/input.txt
```

or

```text
java hash.Digest hash/input.txt MD5
```

### **Listing 9.16** hash/Digest.java

```java
package hash;

import java.io.*;
import java.nio.file.*;
import java.security.*;

/**
 * This program computes the message digest of a file.
 * @version 1.20 2012-06-16
 * @author Cay Horstmann
 */
public class Digest
{
   /**
    * @param args args[0] is the filename, args[1] is optionally the algorithm
    * (SHA-1, SHA-256, or MD5)
    */
```

fingerprint. After all, the message digest algorithms are publicly known, and they don't require secret keys. In that case, the recipient of the forged message and the recomputed fingerprint would never know that the message has been altered. Digital signatures solve this problem.

To help you understand how digital signatures work, we'll explain a few concepts from the field called *public key cryptography*. Public key cryptography is based on the notion of a *public key* and *private key*. The idea is that you tell everyone in the world your public key. However, you only hold the private key, and it is important that you safeguard it and don't release it to anyone else. The keys are matched by mathematical relationships, though the exact nature of these relationships is not important to us. (If you are interested, look it up in *The Handbook of Applied Cryptography* at www.cacr.math.uwaterloo.ca/hac.)

The keys are quite long and complex. For example, here is a matching pair of public and private Digital Signature Algorithm (DSA) keys.

```text
Public key:

p: fca682ce8e12caba26efccf7110e526db078b05edecbcd1eb4a208f3ae1617ae01f35b91a47e6df63413c5e12ed089
9bcd132acd50d99151bdc43ee737592e17

q: 962eddcc369cba8ebb260eeb6a126d9346e38c5

g: 678471b27a9cf44ee91a49c5147db1a9aaf244f05a434d6486931d2d14271b9e35030b71fd73da179069b32e293563
0e1c2062354d0da20a6c416e50be794ca4

y: c0b67e6b4ac096eb1a32c5f8c4c1f0e7ef6b9d83232e27d0dbab9ca2d2a8123c3ea0d188b8161a760480fadd040b92
7281dd22cb9bc4df39d7d4d1b977450

Private key:

p: fca682ce8e12caba26efccf7110e526db078b05edecbcd1eb4a208f3ae1617ae01f35b91a47e6df63413c5e12ed089
9bcd132acd50d99151bdc43ee737592e17

q: 962eddcc369cba8ebb260eeb6a126d9346e38c5

g: 678471b27a9cf44ee91a49c5147db1a9aaf244f05a434d6486931d2d14271b9e35030b71fd73da179069b32e293563
0e1c2062354d0da20a6c416e50be794ca4

x: 146c09f881656cc6cf1f27eafc3a91b85ed1d70a
```

It is believed to be practically impossible to compute one key from the other. That is, even though everyone knows your public key, they can't compute your private key in your lifetime, no matter how many computing resources they have available.

It might seem difficult to believe that you can't compute the private key from the public key, but nobody has ever found an algorithm to do this for the encryption algorithms in common use today. If the keys are sufficiently long, brute force—simply trying all possible keys—would require more computers than can be built from all the atoms in the solar system, crunching away for thousands of years. Of course it is possible that someone could come up with algorithms for computing keys that are much more clever than brute force. For example, the RSA algorithm (the encryption algorithm invented by Rivest, Shamir, and Adleman) depends on the difficulty of factoring large numbers. For the last 20 years, many of the best mathematicians have tried to come up with good factoring algorithms, but so far with no success. For that reason, most cryptographers believe that keys with a “modulus” of 2,000 bits or more are currently completely safe from any attack. DSA is believed to be similarly secure.

Figure 9.11 illustrates how the process works in practice.

![](img/7dd923a566750151a3aab0dacd0cdaa5_572_0.png)

**Figure 9.11** Public key signature exchange with DSA

Suppose Alice wants to send Bob a message, and Bob wants to know this message came from Alice and not an impostor. Alice writes the message and signs the message digest with her private key. Bob gets a copy of her public key. Bob then applies the public key to *verify* the signature. If the verification passes, Bob can be assured of two facts:

- The original message has not been altered.
- The message was signed by Alice, the holder of the private key that matches the public key that Bob used for verification.

You can see why the security of private keys is so important. If someone steals Alice's private key, or if a government can require her to turn it over, then she is in trouble. The thief or a government agent can now impersonate her by sending messages, such as money transfer instructions, that others will believe came from Alice.

### 9.4.3 Verifying a Signature

The JDK comes with the `keytool` program, which is a command-line tool to generate and manage a set of certificates. We expect that ultimately the functionality of this tool will be embedded in other, more user-friendly programs. But right now, we'll use `keytool` to show how Alice can sign a document and send it to Bob, and how Bob can verify that the document really was signed by Alice and not an impostor.

The `keytool` program manages *keystores*, databases of certificates and private/public key pairs. Each entry in the keystore has an *alias*. Here is how Alice creates a keystore, `alice.certs`, and generates a key pair with alias `alice`:

```text
keytool -genkeypair -keystore alice.certs -alias alice
```

When creating or opening a keystore, you are prompted for a keystore password. For this example, just use secret. If you were to use the `keytool`-generated keystore for any serious purpose, you would need to choose a good password and safeguard this file.

When generating a key, you are prompted for the following information:

```text
Enter keystore password: secret
Reenter new password: secret
What is your first and last name?
  [Unknown]:  Alice Lee
```
