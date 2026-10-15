# Cryptographic Hash Algorithms

The abstract class System.Security.Cryptography.HashAlgorithm represents the concept of cryptographic hash algorithms within the .NET Framework. The framework provides eight classes that extend the HashAlgorithm abstract class:

+   - MD5CryptoServiceProvider (extends abstract class MD5)
+   - RIPEMD160Managed (extends abstract class RIPEMD160)
+   - SHA1CryptoServiceProvider (extends abstract class SHA1)
+   - SHA256Managed (extends abstract class SHA256)
+   - SHA384Managed (extends abstract class SHA384)
+   - SHA512Managed (extends abstract class SHA512)
+   - HMACSHA1 (extends abstract class KeyedHashAlgorithm)
+   - MACTripleDES (extends abstract class KeyedHashAlgorithm)

The last two classes belong to a class of algorithm called keyed hash algorithms. The keyed hashes extend the concept of the cryptographic hash with the use of a shared secret key. This is used for computing the hash of data transported over an unsecured channel.

To demonstrate this, a hashing example is available as part of the code download. The TestHashKey.vb file is part of the ProVB_Security solution. This class can be called using the following line of code:

```
TextBox1.Text = TestHashKey.Main("..\..\TestHashKey.vb")
```

Code snippet from TestHashKey.vb

Calling the shared method Main using the line of code above from the ButtonTest_Click event handler will run the following example code telling it to encrypt a copy of the source file TestHashKey.vb:

```
'TestHashKey.vb
Imports System
Imports System.IO
Imports System.Security.Cryptography
Imports System.Text

Public Class TestHashKey
    Public Shared Function Main(ByVal pathToFileToProtect As String) As String
        Dim key() As Byte = Encoding.ASCII.GetBytes("My Secret Key".ToCharArray())
        Dim hmac As HMACSHA1 = New HMACSHA1(key)
        Dim fs As FileStream = File.OpenRead(pathToFileToProtect)
        Dim hash() As Byte = hmac.ComputeHash(fs)
        Dim b64 As String = Convert.ToBase64String(hash)
        fs.Close()
        Return b64
    End Function
End Class
```

Code snippet from TestHashKey.vb

The preceding snippet creates the object instance of the .NET SDK Framework class with a salt (a random secret to confuse a snooper). The next four lines compute the hash, encode the binary hash into a printable Base64 format, close the file, and then return the Base64 encoded string. Running this will result in the hashed output shown in Figure 32-8.

![](bbox=[0.49, 0.735, 0.78, 0.825])

# FIGURE 32-8