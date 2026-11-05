# Chapter 148: Hash Functions

# Section 148.1: PBKDF2 for Password Hashing

PBKDF2 ("Password-Based Key Derivation Function 2") is one of the recommended hash-functions for password-hashing. It is part of rfc-2898.

.NET's Rfc2898DeriveBytes-Class is based upon HMACSHA1.

```
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
```

PBKDF2 requires a salt and the number of iterations.

# Iterations:

A high number of iterations will slow the algorithm down, which makes password cracking a lot harder. A high number of iterations is therefor recommended. PBKDF2 is order of magnitudes slower than MD5 for example.

# Salt:

A salt will prevent the lookup of hash values in rainbow tables. It has to be stored alongside the password hash. One salt per password (not one global salt) is recommended.

# Section 148.2: Complete Password Hashing Solution using Pbkdf2

```
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
```
```