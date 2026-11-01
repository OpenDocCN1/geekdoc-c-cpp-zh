```
```
byte[] signature = signingAlg.SignData(data);
signingAlg.Clear();
}
return signature;
```
```

For verification if the signature was really from Alice, Bob checks the signature by using the public key from Alice. The byte array containing the public key blob can be imported to a CngKey object with the static Import() method. The ECDsaCng class is then used to verify the signature by invoking VerifyData().

```
```
static bool VerifySignature(byte[] data, byte[] signature, byte[] pubKey)
{
    bool retValue = false;
    using (CngKey key = CngKey.Import(pubKey, CngKeyBlobFormat.GenericPublicBlob))
    {
        var signingAlg = new ECDsaCng(key);
        retValue = signingAlg.VerifyData(data, signature);
        signingAlg.Clear();
    }
    return retValue;
}
```
```

# Key Exchange and Secure Transfer

Let's get into a more complex example to exchange a symmetric key for a secure transfer by using the Diffie Hellman algorithm. In the Main() method, you can see the main functionality. Alice creates an encrypted message and sends the encrypted message to Bob. Before that, key pairs are created for Alice and Bob. Bob gets access only to Alice's public key, and Alice gets access only to Bob's public key.

```
```
using System;
using System.IO;
using System.Security.Cryptography;
using System.Text;

namespace Wrox.ProCSharp.Security
{
    class Program
    {
        static CngKey aliceKey;
        static CngKey bobKey;
        static byte[] alicePubKeyBlob;
        static byte[] bobPubKeyBlob;

        static void Main()
        {
            CreateKeys();
            byte[] encryptedData = AliceSendsData("secret message");
            BobReceivesData(encryptedData);
        }
    }
}
```
```

code snippet SecureTransfer/Program.cs

In the implementation of the CreateKeys() method, keys are created to be used with the EC Diffie Hellman 256 algorithm.

```
```
private static void CreateKeys()
{
    aliceKey = CngKey.Create(CngAlgorithm.ECDiffieHellmanP256);
    bobKey = CngKey.Create(CngAlgorithm.ECDiffieHellmanP256);
```
```