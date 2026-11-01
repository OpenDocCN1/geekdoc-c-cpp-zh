First, take a look at the major steps in the Main() method: Alice's keys are created, and the string "Alice" is signed and finally verified if the signature is really from Alice by using the public key. The message that is signed is converted to a byte array by using the Encoding class. To write the encrypted signature to the console, the byte array that contains the signature is converted to a string with the method Convert.ToBase64String().

> Never convert encrypted data to a string using the Encoding class. The Encoding class verifies and converts invalid values that are not allowed with Unicode, and thus converting the string back to a byte array yields a different result.

```
```csharp
using System;
using System.Security.Cryptography;
using System.Text;

namespace Wrox.ProCSharp.Security
{
    class Program
    {
        internal static CngKey aliceKeySignature;
        internal static byte[] alicePubKeyBlob;

        static void Main()
        {
            CreateKeys();

            byte[] aliceData = Encoding.UTF8.GetBytes("Alice");
            byte[] aliceSignature = CreateSignature(aliceData, aliceKeySignature);
            Console.WriteLine("Alice created signature: {0}", Convert.ToBase64String(aliceSignature));

            if (VerifySignature(aliceData, aliceSignature, alicePubKeyBlob))
            {
                Console.WriteLine("Alice signature verified successfully");
            }
        }
    }
}
```
```

Code snippet SigningDemo/Program.cs

CreateKeys() is the method that creates a new key pair for Alice. This key pair is stored in a static field, so it can be accessed from the other methods. The Create() method of CngKey gets the algorithm as an argument to define a key pair for the algorithm. With the Export() method, the public key of the key pair is exported. This public key can be given to Bob for the verification of the signature. Alice keeps the private key. Instead of creating a key pair with the CngKey class, you can open existing keys that are stored in the key store. Usually Alice would have a certificate containing a key pair in her private store, and the store could be accessed with CngKey.Open().

```
```csharp
static void CreateKeys()
{
    aliceKeySignature = CngKey.Create(CngAlgorithm.ECDSA_P256);
    alicePubKeyBlob = aliceKeySignature.Export(CngKeyBlobFormat.GenericPublicBlob);
}
```
```

With the key pair, Alice can create the signature using the ECDsaCng class. The constructor of this class receives the CngKey from Alice that contains both the public and private key. The private key is used, signing the data with the SignData() method.

```
```csharp
static byte[] CreateSignature(byte[] data, CngKey key)
{
    var signingAlg = new ECDsaCng(key);
```
```