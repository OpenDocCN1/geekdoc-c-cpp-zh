The arguments of the Sign Tool command are described as follows:

+   - **command** – Provides a command flag to specify the operation to be performed on a file, such as catdb, sign, signwizard, timestamp, and verify
+   - **options** – Provides an option flag to modify a command flag, such as catdb options (/d, /g, /u), sign options (/a, /c, /d, /f), timestamp option (/t), verify options (/a, /ad, /r, /o), and global options (/q, /v)
+   - **file_name** – Provides the location of the file to be signed

# NOTE

> Sign Tool is not supported on Windows NT, Windows Me, Windows 95, and Windows 98.

# Strong Names

To understand the concept of strong naming assemblies, you should have a sound knowledge of public key cryptography. So, let’s first discuss the public key cryptography with the help of an example. Just imagine that you have a pair of keys where something locked by one key can only be opened by the other, and vice versa. You have your name scribed on both the keys. Now imagine that your friend has a similar kind of key pair with his name scribed on them. Let’s say that both of you make a copy of only one of the keys in each pair and exchange them with each other. Now if you send your friend a message locked with the copy of his key that he gave you, no one else but he will be able to unlock it, as only he has the unlocking key of the pair of keys.

In the preceding example, the keys that are copied and distributed are called public keys; while the ones that are kept safe from others are private keys. Exchanging information in the arrangement of such locking/unlocking key pairs serves two purposes—firstly, it prevents anyone from eavesdropping on your message; secondly, it assures the receiver that the message has been sent by an authenticated party.

When you make a strong name key pair file, the sn.exe utility writes a unique public–private key pair to the generated file. Mentioning the key file in the AssemblyInfo.cs file makes the compiler lock the assembly against any further changes by creating a hash of all files that belong to that assembly. The compiler then signs the hash using the private key. This private key is not written to the assembly, but kept in the key file only. It can be verified with the public key, which is written to the assembly and can be extracted by any application that refers to the assembly. The initial part (called the token) of this public key is written to the assembly manifest of the clients that refer to it. To make any changes to the assembly, you need to mention the key pair file that has the private key for the compiler to be able to update the hash and sign it again. Therefore, you need to secure the key pair file from unauthorized access.

A strong name is composed of the following components:

+   - **Simple name** – Provides a text string specifying the name of the assembly.
+   - **Public key token** – Provides the public key value of an assembly, and is assigned using the AssemblyKeyFile attribute.
+   - **Version number** – Provides the major and minor version numbers of the assembly, including a revision and build number. It is assigned using the AssemblyVersion attribute.
+   - **Culture information** – Provides information on the culture or language for localization purposes. You can assign the culture of the assembly by using the AssemblyCulture attribute.
+   - **Digital signature** – Is created using a hash of the assembly’s content and the private key.

GAC performs integrity checks on all the assemblies installed in it. You are required to strong name your assemblies before putting them in the GAC. If any unauthorized user tries to access your assembly, then GAC will detect this unauthorized access, and would not allow the user to update the hash in the absence of the key pair file.

# Delayed Signing

Delayed Signing is a technique in which the assemblies are partially signed when they are still in the development phase. Delayed Signing prevents tampering an assembly by unauthorized users. The main aim of Delayed Signing is to protect and control the private key of an assembly and use it only during the development process. This technique is useful in a situation where you have to provide your assembly to other in-house