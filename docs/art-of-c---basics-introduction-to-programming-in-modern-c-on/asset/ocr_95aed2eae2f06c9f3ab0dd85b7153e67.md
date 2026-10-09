# 10.3. Exercises

One thing to note from the output of this sample code is that the hash values are very different even for the rather similar input strings. For instance, for "hello world." and "hello world!", we get two completely different hash values.

```
input1 = hello world.
hashed1 = 3C4292AE95BE58E0C58E4E5511F09647
```

```
input = hello world!
hashed = FC3FF98E8C6A0D3087D515C0473F8677
```

For an input string, "hello world", its MD5 hash value is 5EB63BBBE01EED093CB22BB8F5ACDC3, another completely different value.

This is a characteristic of a good hashing function. One cannot easily guess an arbitrary input based on the hash values of any known similar inputs.

# Summary

We demonstrated, in this lesson, the use of some simple APIs from the System.Text and System.Security.Cryptography namespaces in .NET.

We introduced the extension methods in C#. We also showed another use of the using keyword in the context of the IDisposable type variables.

# 10.3. Exercises

+   1. Write a program that accepts a string as a command line argument and produces the MD5 hash for the given string.
2. Write a similar program that produces the SHA256 hash value. Here’s a relevant doc: [SHA256 Class (https://docs.microsoft.com/en-us/dotnet/api/system.security.cryptography.sha256?view=net-5.0)].