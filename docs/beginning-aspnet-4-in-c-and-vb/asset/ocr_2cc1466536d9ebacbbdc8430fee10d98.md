Comparing the symmetric keys created from Alice and Bob shows that the same key value gets created.
Using this symmetric key and the initialization vector, the message from Alice can be decrypted with the AesCryptoServiceProvider class.

```
private static void BobReceivesData(byte[] encryptedData)
{
    Console.WriteLine("Bob receives encrypted data");
    byte[] rawData = null;

    var aes = new AesCryptoServiceProvider();

    int nBytes = aes.BlockSize / 8;
    byte[] iv = new byte[nBytes];
    for (int i = 0; i < iv.Length; i++)
        iv[i] = encryptedData[i];

    using (var bobAlgorithm = new ECDiffieHellmanCng(bobKey))
    using (CngKey alicePubKey = CngKey.Import(alicePubKeyBlob,
        CngKeyBlobFormat.EccPublicBlob))
    {
        byte[] symmKey = bobAlgorithm.DeriveKeyMaterial(alicePubKey);
        Console.WriteLine("Bob creates this symmetric key with " +
            "Alices public key information: {0}",
            Convert.ToBase64String(symmKey));

        aes.Key = symmKey;
        aes.IV = iv;

        using (ICryptoTransform decryptor = aes.CreateDecryptor())
        using (MemoryStream ms = new MemoryStream())
        {
            var cs = new CryptoStream(ms, decryptor, CryptoStreamMode.Write);
            cs.Write(encryptedData, nBytes, encryptedData.Length - nBytes);
            cs.Close();

            rawData = ms.ToArray();

            Console.WriteLine("Bob decrypts message to: {0}",
                Encoding.UTF8.GetString(rawData));
        }
    }
    aes.Clear();
}
```

When you run the application, you can see output similar to the following on the console. The message from Alice is encrypted, and decrypted by Bob with the securely exchanged symmetric key.

Alice sends message: secret message
Alice creates this symmetric key with Bobs public key information:
5NWat8emZFCYoIIla9SIVn4AXy4iALRATFo4iVbw=
Alice: message is encrypted: 3CSU9CpXmoPtk3Bw2V0TS P0ojg rycSR7Te8z tau5N0=

Bob receives encrypted message
Bob creates this symmetric key with Alices public key information:
5NWat8emZFCYoIIla9SIVn4AXy4iALRATFo4iVbw=
Bob decrypts message to: secret message

# ACCESS CONTROL TO RESOURCES

With the operating system, resources such as files and registry keys, as well as handles of a named pipe, are secured by using an access control list. Figure 21-3 shows the structure of how this maps. The resource has a security descriptor associated. The security descriptor contains information about the owner of the resource