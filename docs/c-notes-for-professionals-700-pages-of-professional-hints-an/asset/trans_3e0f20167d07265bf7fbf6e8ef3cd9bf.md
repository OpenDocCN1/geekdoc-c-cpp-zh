
## 第 148 章：哈希函数

### 第 148.1 节：用于密码哈希的 PBKDF2

PBKDF2（“基于密码的密钥派生函数 2”）是用于密码哈希的推荐哈希函数之一。它属于 RFC 2898 的一部分。

.NET 的 Rfc2898DeriveBytes 类基于 HMACSHA1。

```csharp
using System.Security.Cryptography;

...

public const int SALT_SIZE = 24; // size in bytes
public const int HASH_SIZE = 24; // size in bytes
public const int ITERATIONS = 100000; // number of pbkdf2 iterations

public static byte[] CreateHash(string input)
{
    // Generate a salt
    RNGCryptoServiceProvider provider = new RNGCryptoServiceProvider();
    byte[] salt = new byte[SALT_SIZE];
    provider.GetBytes(salt);

    // Generate the hash
    Rfc2898DeriveBytes pbkdf2 = new Rfc2898DeriveBytes(input, salt, ITERATIONS);
    return pbkdf2.GetBytes(HASH_SIZE);
}
```

PBKDF2 需要盐和迭代次数。

### 迭代次数：

较高的迭代次数会降低算法速度，从而使密码破解困难得多。因此建议使用较高的迭代次数。例如，PBKDF2 比 MD5 慢几个数量级。

### 盐：

盐可以防止在彩虹表中查找哈希值。它必须与密码哈希一起存储。建议每个密码使用一个盐（而不是一个全局盐）。

### 第 148.2 节：使用 Pbkdf2 的完整密码哈希解决方案

```csharp
using System;
using System.Linq;
using System.Security.Cryptography;

namespace YourCryptoNamespace
{
    /// <summary>
    /// Salted password hashing with PBKDF2-SHA1.
    /// Compatibility: .NET 3.0 and later.
    /// </summary>
    /// <remarks>See http://crackstation.net/hashing-security.htm for much more on password hashing.</remarks>
    public static class PasswordHashProvider
{
    /// <summary>
    /// The salt byte size, 64 length ensures safety but could be increased / decreased
    /// </summary>
    private const int SaltByteSize = 64;
    /// <summary>
    /// The hash byte size,
    /// </summary>
    private const int HashByteSize = 64;
    /// <summary>
    /// High iteration count is less likely to be cracked
    /// </summary>
    private const int Pbkdf2Iterations = 10000;

    /// <summary>
    /// Creates a salted PBKDF2 hash of the password.
    /// </summary>
    /// <remarks>
    /// The salt and the hash have to be persisted side by side for the password. They could be
    persisted as bytes or as a string using the convenience methods in the next class to convert from
    byte[] to string and later back again when executing password validation.
    /// </remarks>
    /// <param name="password">The password to hash.</param>
    /// <returns>The hash of the password.</returns>
    public static PasswordHashContainer CreateHash(string password)
    {
        // Generate a random salt
        using (var csprng = new RNGCryptoServiceProvider())
        {
            // create a unique salt for every password hash to prevent rainbow and dictionary based
            attacks
            var salt = new byte[SaltByteSize];
            csprng.GetBytes(salt);

            // Hash the password and encode the parameters
            var hash = Pbkdf2(password, salt, Pbkdf2Iterations, HashByteSize);

            return new PasswordHashContainer(hash, salt);
        }
    }

    /// <summary>
    /// Recreates a password hash based on the incoming password string and the stored salt
    /// </summary>
    /// <param name="password">The password to check.</param>
    /// <param name="salt">The salt existing.</param>
    /// <returns>The generated hash based on the password and salt</returns>
    public static byte[] CreateHash(string password, byte[] salt)
    {
        // Extract the parameters from the hash
        return Pbkdf2(password, salt, Pbkdf2Iterations, HashByteSize);
    }

    /// <summary>
    /// Validates a password given a hash of the correct one.
    /// </summary>
    /// <param name="password">The password to check.</param>
    /// <param name="salt">The existing stored salt.</param>
    /// <param name="correctHash">The hash of the existing password.</param>
    /// <returns><c>true</c> if the password is correct. <c>false</c> otherwise.</returns>
    public static bool ValidatePassword(string password, byte[] salt, byte[] correctHash)
    {
        // Extract the parameters from the hash
byte[] testHash = Pbkdf2(password, salt, Pbkdf2Iterations, HashByteSize);
return CompareHashes(correctHash, testHash);
}
/// <summary>
/// Compares two byte arrays (hashes)
/// </summary>
/// <param name="array1">The array1.</param>
/// <param name="array2">The array2.</param>
/// <returns><c>true</c> if they are the same, otherwise <c>false</c></returns>
public static bool CompareHashes(byte[] array1, byte[] array2)
{
    if (array1.Length != array2.Length) return false;
    return !array1.Where((t, i) => t != array2[i]).Any();
}
/// <summary>
/// Computes the PBKDF2-SHA1 hash of a password.
/// </summary>
/// <param name="password">The password to hash.</param>
/// <param name="salt">The salt.</param>
/// <param name="iterations">The PBKDF2 iteration count.</param>
/// <param name="outputBytes">The length of the hash to generate, in bytes.</param>
/// <returns>A hash of the password.</returns>
private static byte[] Pbkdf2(string password, byte[] salt, int iterations, int outputBytes)
{
    using (var pbkdf2 = new Rfc2898DeriveBytes(password, salt))
    {
        pbkdf2.IterationCount = iterations;
        return pbkdf2.GetBytes(outputBytes);
    }
}
/// <summary>
/// Container for password hash and salt and iterations.
/// </summary>
public sealed class PasswordHashContainer
{
    /// <summary>
    /// Gets the hashed password.
    /// </summary>
    public byte[] HashedPassword { get; private set; }
    /// <summary>
    /// Gets the salt.
    /// </summary>
    public byte[] Salt { get; private set; }

    /// <summary>
    /// Initializes a new instance of the <see cref="PasswordHashContainer" /> class.
    /// </summary>
    /// <param name="hashedPassword">The hashed password.</param>
    /// <param name="salt">The salt.</param>
    public PasswordHashContainer(byte[] hashedPassword, byte[] salt)
    {
        this.HashedPassword = hashedPassword;
        this.Salt = salt;
    }
}
/// <summary>
/// Convenience methods for converting between hex strings and byte array.
/// </summary>
```

```csharp
public static class ByteConverter
{
    /// <summary>
    /// Converts the hex representation string to an array of bytes
    /// </summary>
    /// <param name="hexedString">The hexed string.</param>
    /// <returns></returns>
    public static byte[] GetHexBytes(string hexedString)
    {
        var bytes = new byte[hexedString.Length / 2];
        for (var i = 0; i < bytes.Length; i++)
        {
            var strPos = i * 2;
            var chars = hexedString.Substring(strPos, 2);
            bytes[i] = Convert.ToByte(chars, 16);
        }
        return bytes;
    }
    /// <summary>
    /// Gets a hex string representation of the byte array passed in.
    /// </summary>
    /// <param name="bytes">The bytes.</param>
    public static string GetHexString(byte[] bytes)
    {
        return BitConverter.ToString(bytes).Replace("-", "").ToUpper();
    }
}
```

```csharp
/*
 * Password Hashing With PBKDF2 (http://crackstation.net/hashing-security.htm).
 * Copyright (c) 2013, Taylor Hornby
 * All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions are met:
 *
 * 1. Redistributions of source code must retain the above copyright notice,
 * this list of conditions and the following disclaimer.
 *
 * 2. Redistributions in binary form must reproduce the above copyright notice,
 * this list of conditions and the following disclaimer in the documentation
 * and/or other materials provided with the distribution.
 *
 * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
 * AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
 * IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
 * ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE
 * LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
 * CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
 * SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
 * INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
 * CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
 * ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
 * POSSIBILITY OF SUCH DAMAGE.
 */
```

请参阅这个优秀的资源 [Crackstation - 加盐密码哈希 - 正确做法](http://crackstation.net/hashing-security.htm) 以了解更多信息。
此解决方案的一部分（哈希函数）基于该站点的代码。

