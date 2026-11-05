```
```csharp
binaryWriter.Write(
    encryptedMessage,
    nonSecretPayloadLength + iv.Length,
    encryptedMessage.Length - nonSecretPayloadLength - iv.Length - sentTag.Length
);
}
//Return Plain Text
return plainTextStream.ToArray();
}
}
}

public static byte[] SimpleEncryptWithPassword(byte[] secretMessage, string password, byte[]
nonSecretPayload = null)
{
    nonSecretPayload = nonSecretPayload ?? new byte[] {};

    //User Error Checks
    if (string.IsNullOrWhiteSpace(password) || password.Length < MinPasswordLength)
        throw new ArgumentException(String.Format("Must have a password of at least {0} characters!", MinPasswordLength), "password");

    if (secretMessage == null || secretMessage.Length ==0)
        throw new ArgumentException("Secret Message Required!", "secretMessage");

    var payload = new byte[(SaltBitSize / 8 * 2) + nonSecretPayload.Length];

    Array.Copy(nonSecretPayload, payload, nonSecretPayload.Length);
    int payloadIndex = nonSecretPayload.Length;

    byte[] cryptKey;
    byte[] authKey;
    //Use Random Salt to prevent pre-generated weak password attacks.
    using (var generator = new Rfc2898DeriveBytes(password, SaltBitSize / 8, Iterations))
    {
        var salt = generator.Salt;

        //Generate Keys
        cryptKey = generator.GetBytes(KeyBitSize / 8);

        //Create Non Secret Payload
        Array.Copy(salt, 0, payload, payloadIndex, salt.Length);
        payloadIndex += salt.Length;
    }

    //Deriving separate key, might be less efficient than using HKDF,
    //but now compatible with RNEncryptor which had a very similar wireformat and requires less
    code than HKDF.
    using (var generator = new Rfc2898DeriveBytes(password, SaltBitSize / 8, Iterations))
    {
        var salt = generator.Salt;

        //Generate Keys
        authKey = generator.GetBytes(KeyBitSize / 8);

        //Create Rest of Non Secret Payload
        Array.Copy(salt, 0, payload, payloadIndex, salt.Length);
    }

    return SimpleEncrypt(secretMessage, cryptKey, authKey, payload);
}
```
```