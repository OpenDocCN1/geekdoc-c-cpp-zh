```
```csharp
var cipherText = Convert.FromBase64String(encryptedMessage);
var plainText = SimpleDecrypt(cipherText, key, nonSecretPayloadLength);
return plainText == null ? null : Encoding.UTF8.GetString(plainText);
}

/// <summary>
/// Simple Encryption And Authentication (AES-GCM) of a UTF8 String
/// using key derived from a password (PBKDF2).
/// </summary>
/// <param name="secretMessage">The secret message.</param>
/// <param name="password">The password.</param>
/// <param name="nonSecretPayload">The non secret payload.</param>
/// <returns>
/// Encrypted Message
/// </returns>
/// <remarks>
/// Significantly less secure than using random binary keys.
/// Adds additional non secret payload for key generation parameters.
/// </remarks>
public static string SimpleEncryptWithPassword(string secretMessage, string password,
    byte[] nonSecretPayload = null)
{
    if (string.IsNullOrEmpty(secretMessage))
        throw new ArgumentException("Secret Message Required!", "secretMessage");

    var plainText = Encoding.UTF8.GetBytes(secretMessage);
    var cipherText = SimpleEncryptWithPassword(plainText, password, nonSecretPayload);
    return Convert.ToBase64String(cipherText);
}

/// <summary>
/// Simple Decryption and Authentication (AES-GCM) of a UTF8 message
/// using a key derived from a password (PBKDF2)
/// </summary>
/// <param name="encryptedMessage">The encrypted message.</param>
/// <param name="password">The password.</param>
/// <param name="nonSecretPayloadLength">Length of the non secret payload.</param>
/// <returns>
/// Decrypted Message
/// </returns>
/// <exception cref="System.ArgumentException">Encrypted Message Required!</exception>
/// <remarks>
/// Significantly less secure than using random binary keys.
/// </remarks>
public static string SimpleDecryptWithPassword(string encryptedMessage, string password,
    int nonSecretPayloadLength = 0)
{
    if (string.IsNullOrWhiteSpace(encryptedMessage))
        throw new ArgumentException("Encrypted Message Required!", "encryptedMessage");

    var cipherText = Convert.FromBase64String(encryptedMessage);
    var plainText = SimpleDecryptWithPassword(cipherText, password, nonSecretPayloadLength);
    return plainText == null ? null : Encoding.UTF8.GetString(plainText);
}

public static byte[] SimpleEncrypt(byte[] secretMessage, byte[] key, byte[] nonSecretPayload =
null)
{
    //User Error Checks
    if (key == null || key.Length != KeyBitSize / 8)
```
```