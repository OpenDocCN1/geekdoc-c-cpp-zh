```csharp
//Decrypt Cipher Text
var cipherText = cipherReader.ReadBytes(encryptedMessage.Length - nonSecretPayloadLength - nonce.Length);
var plainText = new byte[cipher.GetOutputSize(cipherText.Length)];

try
{
    var len = cipher.ProcessBytes(cipherText, 0, cipherText.Length, plainText, 0);
    cipher.DoFinal(plainText, len);
}
catch (InvalidCipherTextException)
{
    //Return null if it doesn't authenticate
    return null;
}

return plainText;
}

public static byte[] SimpleEncryptWithPassword(byte[] secretMessage, string password, byte[] nonSecretPayload = null)
{
    nonSecretPayload = nonSecretPayload ?? new byte[] {};

    //User Error Checks
    if (string.IsNullOrWhiteSpace(password) || password.Length < MinPasswordLength)
        throw new ArgumentException(String.Format("Must have a password of at least {0} characters!", MinPasswordLength), "password");

    if (secretMessage == null || secretMessage.Length == 0)
        throw new ArgumentException("Secret Message Required!", "secretMessage");

    var generator = new Pkcs5S2ParametersGenerator();

    //Use Random Salt to minimize pre-generated weak password attacks.
    var salt = new byte[SaltBitSize / 8];
    Random.NextBytes(salt);

    generator.Init(
        PbeParametersGenerator.Pkcs5PasswordToBytes(password.ToCharArray()),
        salt,
        Iterations);

    //Generate Key
    var key = (KeyParameter)generator.GenerateDerivedMacParameters(KeyBitSize);

    //Create Full Non Secret Payload
    var payload = new byte[salt.Length + nonSecretPayload.Length];
    Array.Copy(nonSecretPayload, payload, nonSecretPayload.Length);
    Array.Copy(salt,0, payload,nonSecretPayload.Length, salt.Length);

    return SimpleEncrypt(secretMessage, key.GetKey(), payload);
}

public static byte[] SimpleDecryptWithPassword(byte[] encryptedMessage, string password, int nonSecretPayloadLength = 0)
{
    //User Error Checks
    if (string.IsNullOrWhiteSpace(password) || password.Length < MinPasswordLength)
        throw new ArgumentException(String.Format("Must have a password of at least {0} characters!", MinPasswordLength), "password");

    if (encryptedMessage == null || encryptedMessage.Length == 0)
        throw new ArgumentException("Encrypted Message Required!", "encryptedMessage");

    var generator = new Pkcs5S2ParametersGenerator();

    //Grab Salt from Payload
    var salt = new byte[SaltBitSize / 8];
    Array.Copy(encryptedMessage, nonSecretPayloadLength, salt, 0, salt.Length);

    generator.Init(
        PbeParametersGenerator.Pkcs5PasswordToBytes(password.ToCharArray()),
        salt,
        Iterations);

    //Generate Key
    var key = (KeyParameter)generator.GenerateDerivedMacParameters(KeyBitSize);

    return SimpleDecrypt(encryptedMessage, key.GetKey(), salt.Length + nonSecretPayloadLength);
}
}
```

## Section 150.2: Introduction to Symmetric and Asymmetric Encryption

You can improve the security for data transit or storing by implementing encrypting techniques. Basically there are two approaches when using System.Security.Cryptography: symmetric and asymmetric.

### Symmetric Encryption

This method uses a private key in order to perform the data transformation.

Pros:

- Symmetric algorithms consume less resources and are faster than asymmetric ones.
- The amount of data you can encrypt is unlimited.

Cons:

- Encryption and decryption use the same key. Someone will be able to decrypt your data if the key is compromised.
- You could end up with many different secret keys to manage if you choose to use a different secret key for different data.

Under System.Security.Cryptography you have different classes that perform symmetric encryption, they are known as block ciphers:

- AesManaged (AES algorithm).
- AesCryptoServiceProvider (AES algorithm) FIPS 140-2 compliant.
- DESCryptoServiceProvider (DES algorithm).
- RC2CryptoServiceProvider (Rivest Cipher 2 algorithm).
- RijndaelManaged (AES algorithm). Note: RijndaelManaged is not FIPS-197 compliant.
- TripleDES (TripleDES algorithm).

### Asymmetric Encryption

This method uses a combination of public and private keys in order to perform the data transformation.

Pros:

- It uses larger keys than symmetric algorithms, thus they are less susceptible to being cracked by using brute force.
- It is easier to guarantee who is able to encrypt and decrypt the data because it relies on two keys (public and private).

Cons:

- There is a limit on the amount of data that you can encrypt. The limit is different for each algorithm and is typically proportional with the key size of the algorithm. For example, an RSA CryptoServiceProvider object with a key length of 1,024 bits can only encrypt a message that is smaller than 128 bytes.
- Asymmetric algorithms are very slow in comparison to symmetric algorithms.

Under System.Security.Cryptography you have access to different classes that perform asymmetric encryption:

- DSACryptoServiceProvider (Digital Signature Algorithm algorithm)
- RSACryptoServiceProvider (RSA Algorithm algorithm)

## Section 150.3: Simple Symmetric File Encryption

The following code sample demonstrates a quick and easy means of encrypting and decrypting files using the AES symmetric encryption algorithm.

The code randomly generates the Salt and Initialization Vectors each time a file is encrypted, meaning that encrypting the same file with the same password will always lead to different output. The salt and IV are written to the output file so that only the password is required to decrypt it.

```
public static void ProcessFile(string inputPath, string password, bool encryptMode, string outputPath)
{
    using (var cypher = new AesManaged())
    using (var fsIn = new FileStream(inputPath, FileMode.Open))
    using (var fsOut = new FileStream(outputPath, FileMode.Create))
    {
        const int saltLength = 256;
        var salt = new byte[saltLength];
        var iv = new byte[cypher.BlockSize / 8];

        if (encryptMode)
        {
            // Generate random salt and IV, then write them to file
            using (var rng = new RNGCryptoServiceProvider())
            {
                rng.GetBytes(salt);
                rng.GetBytes(iv);
            }
            fsOut.Write(salt, 0, salt.Length);
            fsOut.Write(iv, 0, iv.Length);
        }
        else
        {
            // Read the salt and IV from the file
            fsIn.Read(salt, 0, saltLength);
            fsIn.Read(iv, 0, iv.Length);
        }

        // Generate a secure password, based on the password and salt provided
        var pdb = new Rfc2898DeriveBytes(password, salt);
        var key = pdb.GetBytes(cypher.KeySize / 8);

        // Encrypt or decrypt the file
        using (var cryptoTransform = encryptMode
            ? cypher.CreateEncryptor(key, iv)
            : cypher.CreateDecryptor(key, iv))
        using (var cs = new CryptoStream(fsOut, cryptoTransform, CryptoStreamMode.Write))
        {
            fsIn.CopyTo(cs);
        }
    }
}
```

## Section 150.4: Cryptographically Secure Random Data

There are times when the framework's Random() class may not be considered random enough, given that it is based on a pseudo-random number generator. The framework's Crypto classes do, however, provide something more robust in the form of RNGCryptoServiceProvider.

The following code samples demonstrate how to generate Cryptographically Secure byte arrays, strings and numbers.

### Random Byte Array

```
public static byte[] GenerateRandomData(int length)
{
    var rnd = new byte[length];
    using (var rng = new RNGCryptoServiceProvider())
        rng.GetBytes(rnd);
    return rnd;
}
```

### Random Integer (with even distribution)

```
public static int GenerateRandomInt(int minVal=0, int maxVal=100)
{
    var rnd = new byte[4];
    using (var rng = new RNGCryptoServiceProvider())
        rng.GetBytes(rnd);
    var i = Math.Abs(BitConverter.ToInt32(rnd, 0));
    return Convert.ToInt32(i % (maxVal - minVal + 1) + minVal);
}
```

### Random String

```
public static string GenerateRandomString(int length, string allowableChars=null)
{
    if (string.IsNullOrEmpty(allowableChars))
        allowableChars = "@ABCDEFGHIJKLMNOPQRSTUVWXYZ";

    // Generate random data
    var rnd = new byte[length];
    using (var rng = new RNGCryptoServiceProvider())
        rng.GetBytes(rnd);
```
