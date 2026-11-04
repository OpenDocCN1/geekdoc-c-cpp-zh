To deploy an assembly as a shared assembly, you need to create a signature for your assembly by performing the following steps:

+   1. Generate a key pair containing a private key and a public key.
+   2. Write the public key to the manifest of the assembly.
+   3. Create a hash of all files belonging to the assembly.
+   4. Sign the hash with the private key (the private key is not stored within the assembly).

These steps guarantee that the assembly cannot be altered in any way, ensuring that the shared assembly you are using is the authentic copy provided by the vendor. The signature can be verified using the public key.

The following sections will show you how to perform each of these steps.

For the client application using the shared assembly, the compiler writes the public key of the shared assembly to the manifest of the client so that it can unique identify the shared assembly (only the last 8 bytes of a hash of a public key are stored; this is known as the public key token and is always unique). When an application loads the shared assembly, it uses the public key stored in the shared assembly to decrypt the encrypted hash and match it against the hash of the shared assembly to ensure that the shared assembly is authentic.

# Creating a Shared Assembly

You'll better understand how to create a shared assembly by actually creating one. In this example, you create a library to perform Base64 encoding and decoding. Basically, Base64 encoding is a technique to encode binary data into a text-based representation so that it can be easily transported over networks and Web Services. A common usage of Base64 is in emails.

Using Visual Studio 2008, create a new Class Library project and name it Base64Codec. In the default Class1.cs, define the Helper class containing two methods — Decode() and Encode():

```
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Base64Codec
{
    public class Helper
    {
        public byte[] Decode(string base64string)
        {
            byte[] binaryData;
            try
            {
                binaryData =
                    Convert.FromBase64String(base64string);
                return binaryData;
            }
        }
    }
```
```