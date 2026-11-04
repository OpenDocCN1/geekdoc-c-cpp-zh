
## Understanding Cryptography

In the world of cryptography, there are two main types of encryption and encryption algorithms — symmetric and asymmetric.

Symmetric encryption is also sometimes known as private key encryption. With private key encryption, you encrypt a secret message using a key that only you know. To decrypt the message, you need to use the same key. Private key encryption is effective only if the key can be kept a secret. If too many people know the key, its effectiveness is reduced.

Imagine that you are trying to send a secret message to your faraway friend, Susan, using a private key. For Susan to decrypt the secret message, she must know the private key. So you need to send it to her. But if the secrecy of the key is compromised somehow (such as through people eavesdropping on your conversation), then the message is no longer secure. Moreover, if Susan tells another friend about the private key, her friend can then also decrypt the message. Despite the potential weakness of private key encryption, it is very easy to implement and, computationally, it does not take up too many resources.

Private key encryption requires that the key used in the encryption process be kept a secret. A more effective way to transport secret messages to your intended recipient is to use asymmetric encryption (also known as public key encryption). In public key encryption, there is a pair of keys involved. This pair, consisting of a private key and a public key, is related mathematically such that messages encrypted with the public key can only be decrypted with the corresponding private key. The contrary is true; messages encrypted with the private key can only be decrypted with the public key. Let's see an example for each scenario.

Before you send a message to Susan, Susan needs to generate the key pair containing the private key and the public key. Susan then freely distributes the public key to you (and all her other friends) but keeps the private key to herself. When you want to send a message to Susan, you use her public key to encrypt the message and then send it to her. Upon receiving the encrypted message, Susan proceeds to decrypt it with her private key. In this case, Susan is the only one who can decrypt the message because the key pair works in such a way that only messages encrypted with the public key can be decrypted with the private key. Also, there is no need to exchange secret keys, thus eliminating the risk of compromising the secrecy of the key.

The reverse can happen. Suppose Susan now sends a message encrypted with her private key to you. To decrypt the message, you need the public key. The scenario may seem redundant because the public key is not a secret; everyone knows it. But using this method guarantees that the message has not been tampered with and that it indeed comes from Susan. If the message had been modified, you would not be able to decrypt it. The fact that you can decrypt the message using the public key proves that the message has not been modified.

In computing, public key cryptography is a secure way to encrypt information. However, it is computationally expensive, because it is time-consuming to generate the key pairs and to perform encryption and decryption. It is usually used for encrypting a small amount of sensitive information.

To deploy an assembly as a shared assembly, you need to create a signature for your assembly by performing the following steps:

- 1. Generate a key pair containing a private key and a public key.
- 2. Write the public key to the manifest of the assembly.
- 3. Create a hash of all files belonging to the assembly.
- 4. Sign the hash with the private key (the private key is not stored within the assembly).

These steps guarantee that the assembly cannot be altered in any way, ensuring that the shared assembly you are using is the authentic copy provided by the vendor. The signature can be verified using the public key.

The following sections will show you how to perform each of these steps.

For the client application using the shared assembly, the compiler writes the public key of the shared assembly to the manifest of the client so that it can uniquely identify the shared assembly (only the last 8 bytes of a hash of a public key are stored; this is known as the public key token and is always unique). When an application loads the shared assembly, it uses the public key stored in the shared assembly to decrypt the encrypted hash and match it against the hash of the shared assembly to ensure that the shared assembly is authentic.

## Creating a Shared Assembly

You'll better understand how to create a shared assembly by actually creating one. In this example, you create a library to perform Base64 encoding and decoding. Basically, Base64 encoding is a technique to encode binary data into a text-based representation so that it can be easily transported over networks and Web Services. A common usage of Base64 is in emails.

Using Visual Studio 2008, create a new Class Library project and name it Base64Codec. In the default Class1.cs, define the Helper class containing two methods — Decode() and Encode():

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
            catch (Exception)
            {
                return null;
            }
        }

        public string Encode(byte[] binaryData)
        {
            string base64String;
            try
            {
                base64String =
                    Convert.ToBase64String(
                        binaryData, 0, binaryData.Length);
                return base64String;
            }
            catch (Exception)
            {
                return string.Empty;
            }
        }
    }
}
```

## Creating a Strong Name

To create a strong name for the assembly, you need to sign it. The easiest way is to use the Properties page of the project in Visual Studio 2008. Right-click on the project name in Solution Explorer, and select Properties. Select the Signing tab (see Figure 15-28), and check the Sign The Assembly checkbox. Select <New> from the Choose A Strong Name Key File dropdown list to specify a name for the strong name file.

![](img/a977a875c7c627b45d939729705a252e_512_0.png)

Figure 15-28

## Part I: C# Fundamentals

In the Create Strong Name Key dialog (see Figure 15-29), specify a name to store the pair of keys (keyFile.snk, for instance). You also have the option to protect the file with a password. Click OK.

> An SNK file is a binary file containing the pair of public and private keys.

![](img/a977a875c7c627b45d939729705a252e_513_0.png)

Figure 15-29

A strong name file is now created in your project (see Figure 15-30).

![](img/a977a875c7c627b45d939729705a252e_513_1.png)

Figure 15-30

Alternatively, you can also use the command line to generate the strong name file:

```
sn -k KeyFile.snk
```

## Versioning

With .NET, you can create different versions of the same assembly and share them with other applications. To specify version information, you can edit the AssemblyInfo.cs file, located under the Properties item in Solution Explorer (see Figure 15-31).

![](img/a977a875c7c627b45d939729705a252e_513_2.png)

Figure 15-31

Figure 15-33 shows the public key token displayed in the console window. Note this number because you will use it for comparison later.

![](img/a977a875c7c627b45d939729705a252e_515_0.png)

Figure 15-33

## The Global Assembly Cache

Now that you have created a shared assembly, the next task is to put it into the GAC. The GAC is a central repository of .NET assemblies that can be shared by all applications. There are several reasons why you should put your shared assembly into the GAC, some of which are:

- **Security** — Assemblies stored in the GAC are required to be signed with a cryptographic key. This makes it difficult for others to tamper with your assembly, such as replacing or injecting your shared assembly with malicious code.
- **Version management** — Multiple versions of the same assembly can reside in the GAC so that each application can find and use the version of your assembly to which it was compiled. This helps to avoid DLL Hell, where applications compiled to different versions of your assembly can potentially break because they are all forced to use a single version of your assembly.
- **Faster loading** — Assemblies are verified when they are first installed in the GAC, eliminating the need to verify an assembly each time it is loaded from the GAC. This improves the startup speed of your application if you load many shared assemblies.

The GAC is located in <windows_directory>\Assembly. In most cases, it is C:\Windows\Assembly. When you navigate to this folder by using Windows Explorer, the Assembly Cache Viewer launches to display the list of assemblies stored in it (see Figure 15-34).

![](img/a977a875c7c627b45d939729705a252e_515_1.png)

Figure 15-34
