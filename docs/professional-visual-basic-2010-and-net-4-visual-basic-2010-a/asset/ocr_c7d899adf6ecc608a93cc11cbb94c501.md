# TABLE 32-6 (continued)

| PROPERTY | DESCRIPTION |
|---|---|
| PermitOnlySetInstance | Returns a permission set or permission set collection that is part of the permit-only stack frame if a security action has failed |
| RefusedSet | Returns the permissions that were refused by the assembly |
| Source | Gets or sets the name of the application or object that triggered the error |
| Url | Returns the URL of the assembly that caused the exception |
| Zone | Returns the zone of the assembly that caused the exception |

Clearly, you can get your hands on a lot of information if a security exception is thrown in your application. For instance, you can use something similar to the following Catch section of code to check for security errors:

```
Dim myFile as FileInfo

Try
    myFile = _
        My.Computer.FileSystem.GetFileInfo("C:\Test\NoPermission.txt")
Catch ex As Security.SecurityException
    MessageBox.Show(ex.Method.Name.ToString())
End Try
```

# ENCRYPTION BASICS

Rather than present an exposition of cryptography, this section is meant to familiarize you with basic techniques required to deal with .NET security and protect your Web services through encryption. There are four different categories of cryptography: encoding, hashing, and symmetric and asymmetric encryption.

First let’s review each of these four different cryptographic categories. The first is encoding, which, as you may already know, if you are at all familiar with encryption, doesn’t actually protect information. The most common encodings are things like UTF8, UTF7, and Base64 encoding. These encodings are typically used to take information that might interact with a container and hide the special characters. Thus, if you want to embed binary data within an XML file and want to ensure that the binary data won’t interfere with the XML, you can Base64 the data, and it can safely be placed within an XML file.

Encoding is quite common for passing hidden or state data in Web pages, MIME, and XML file formats. For example, in ASP.NET, ViewState is an encoded block of information about the state of an ASP.NET page. However, keep in mind that encoded data, while not immediately humanly readable, uses a public algorithm to create its string. Encoding algorithms are designed to be quickly and easily reversed, and without any form of implied privacy. This means that anyone can reverse the encoded data, so for ASP.NET, ViewState does not protect the data which has been encoded, it just allows for transport of that data. To reiterate, encoding does not protect information.

The next item in the list of cryptography categories is hashing. Hashing algorithms digest sequences of data, creating a “random” output for the input string. A hash has a private key that can be varied by each application using the hash. Using a different key ensures you get different random string representations. While changing a single character will result in an entirely different result, the key to a hash is that there is no way to decrypt the original string from that result. In fact, hashing algorithms are specifically designed to not support the decryption of data once it has been hashed. At the same time, a hash always produces the same result for a given input string.

In terms of degree of security, hash keys are generally judged by the size of the encryption key, with larger keys (512-bit) providing greater security than shorter (128-bit) keys. Two popular hashing algorithms are SHA (Secure Hash Algorithm) and MD5 (Message-Digest algorithm 5). These hash keys are used for everything from saving passwords to signing digital documents; in other words, the hash is generated and encrypted using a private key.