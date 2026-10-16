
asymmetric encryption keys.

With a symmetric key, you can use the same key for encryption and decryption. With asymmetric encryption, different keys are used for encryption and decryption: a public key and a private key. Something encrypted using a public key can be decrypted with the corresponding private key. This also works the other way around: Something encrypted using a private key can be decrypted by using the corresponding public key, but not the private key. It’s practically impossible to calculate the private or public key from the other one.

Public and private keys are always created as a pair. The public key can be made available to everybody, and even put on a website, but the private key must be safely locked away. Following are some examples that demonstrate how public and private keys are used for encryption.

If Alice sends a message to Bob (see Figure 24.1), and she wants to ensure that no one other than Bob can read the message, she uses Bob’s public key. The message is encrypted using Bob’s public key. Bob opens the message and can decrypt it using his secretly stored private key. This key exchange guarantees that no one but Bob can read Alice’s message.

![](img/3d365b72b289213a91ade7eb366b8f35_868_0.png)

## Figure 24.1

There is one problem, however: Bob can’t be sure that the mail comes from Alice. Eve can use Bob’s public key to encrypt messages sent to Bob and pretend to be Alice. We can extend this principle using public/private keys. Let’s start again with Alice sending a message to Bob. Before Alice encrypts the message using Bob’s public key, she adds her signature and encrypts the signature using her own private key. Then she encrypts the mail using Bob’s public key. Therefore, it is guaranteed that no one other than Bob can read the message. When

developed at RSA Laboratories, is faster than SHA1. SHA1 is stronger against brute force attacks. The SHA algorithms were designed by the National Security Agency (NSA). MD5 uses a 128-bit hash size; SHA uses 160 bits. The other SHA algorithms contain the hash size in the name. SHA512 is the strongest of these algorithms, with a hash size of 512 bits; it is also the slowest. RIPEMD160 uses a hash size of 160 bits; it is meant to be a replacement for 128-bit MD4 and MD5. RIPEMD was developed from an EU project named RIPE (Race Integrity Primitives Evaluation).

Symmetric

```
DES DESCryptoServiceProvider TripleDESTripleDESCryptoServiceProvider Aes AesCryptoServiceProvider AesManaged RC2 RC2CryptoServiceProvider Rijndael RijndaelManaged
```

Symmetric key algorithms use the same key for encryption and decryption of data. Data Encryption

## Asymmetric

- DSA
- DSACryptoServiceProvider
- ECDsa
- ECDsaCng
- ECDiffieHellman
- ECDiffieHellmanCng
- RSA
- RSACryptoServiceProvider
- RSACng

Standard (DES is now considered insecure because it uses only 56 bits for the key size and can be broken in less than 24 hours. Triple-DES is the successor to DES and has a key length of 168 bits, but the effective security it provides is only 112-bit. Advanced Encryption Standard (AES) has a key size 128, 192, or 256 bits. Rijndael is very similar to AES but offers more key size options. AES is an encryption standard adopted by the U.S. government.

Asymmetric algorithms use different keys for encryption and decryption. The Rivest, Shamir, Adleman (RSA) algorithm was the first one used for signing as well as encryption. The algorithm is

widely used in e-commerce protocols. RSACng is a class new with .NET 4.6 and .NET 5 Core that is based on a Cryptography Next Generation (CNG) implementation. Digital Signature Algorithm (DSA) is a United States Federal Government standard for digital signatures. Elliptic Curve DSA (ECDSA) and EC Diffie-Hellman use algorithms based on elliptic curve groups. These algorithms are more secure, with shorter key sizes. For example, having a key size of 1024 bits for DSA is similar in security to 160 bits for ECDSA. As a result, ECDSA is much faster. EC Diffie-Hellman is an algorithm used to exchange private keys in

|  |  | secure way over a public channel. |

The following section includes some examples demonstrating how these algorithms can be used programmatically.

## Creating and Verifying a Signature

The first example demonstrates a signature using the ECDSA algorithm, described in the preceding table, for signing. Alice creates a signature that is encrypted with her private key and can be accessed using her public key. This way, it is guaranteed that the signature is from Alice.

The sample application SigningDemo makes use of these dependencies and namespaces:

## Dependencies

- NETStandard.Library
- System.Security.Cryptography.Algorithms
- System.Security.Cryptography.Cng

## Namespaces

- System
- System.Security.Cryptography
- System.Text
- static System.Console

First, take a look at the major steps in the Main method: Alice’s keys are created, and the string "Alice" is signed and then verified to be the signature actually from Alice by using the public key. The message that is signed is converted to a byte array by using the Encoding class. To write the encrypted signature to the console, the byte array that contains the signature is converted to a string with the method Convert.ToBase64String (code file SigningDemo/Program.cs):

```
private CngKey _aliceKeySignature;
private byte[] _alicePubKeyBlob;
static void Main()
{
    var p = new Program();
    p.Run();
}
public void Run()
{
    InitAliceKeys();
    byte[] aliceData = Encoding.UTF8.GetBytes("Alice");
    byte[] aliceSignature = CreateSignature(aliceData, aliceKeySignature);
    WriteLine($"Alice created signature: {Convert.ToBase64String(aliceSignature)}");
    if (VerifySignature(aliceData, aliceSignature, alicePubKeyBlob))
```

```
```csharp
WriteLine("Alice signature verified successfully");
}
}
```
```

> **WARNING** *Never convert encrypted data to a string using the `Encoding` class. The `Encoding` class verifies and converts invalid values that are not allowed with Unicode; therefore, converting the string back to a byte array can yield a different result.*

`InitAliceKeys` is the method that creates a new key pair for Alice. This key pair is stored in a static field, so it can be accessed from the other methods. The `Create` method of `CngKey` gets the algorithm as an argument to define a key pair for the algorithm. With the `Export` method, the public key of the key pair is exported. This public key can be given to Bob for verification of the signature. Alice keeps the private key. Instead of creating a key pair with the `CngKey` class, you can open existing keys that are stored in the key store. Usually Alice would have a certificate containing a key pair in her private store, and the store could be accessed with `CngKey.Open`:

```
```csharp
private void InitAliceKeys()
{
    _aliceKeySignature = CngKey.Create(CngAlgorithm.ECDsaP521);
    _alicePubKeyBlob = aliceKeySignature.Export(CngKeyBlobFormat.GenericPublicBlob);
}
```
```

With the key pair, Alice can create the signature using the `ECDsaCng` class. The constructor of this class receives the `CngKey`—which contains both the public and private keys—from Alice. The private key is used to sign the data with the `SignData` method. The method `SignData` is slightly different with .NET Core. .NET Core requires the algorithm:

```
```csharp
public byte[] CreateSignature(byte[] data, CngKey key)
{
    byte[] signature;
    using (var signingAlg = new ECDsaCng(key))
    {
#if NET46
        signature = signingAlg.SignData(data);
        signingAlg.Clear();
#else
        signature = signingAlg.SignData(data,
            HashAlgorithmName.SHA512);
#endif
    }
    return signature;
}
```
```

To verify that the signature was really from Alice, Bob checks the signature by using the public key from Alice. The byte array containing the public key blob can be imported to a `CngKey` object with the static `Import` method. The `ECDsaCng` class is then used to verify the signature by invoking `VerifyData`:
