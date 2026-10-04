Public key numbers are very big. If you want to, create the file that makes the public and private key, you can use the SN utility to see the actual public key. To do this, you must execute the SN utility with the -p switch to create a file that contains only the public key (MyCompany.PublicKey).¹

```
SN -p MyCompany.snk MyCompany.PublicKey sha256
```

Now, you invoke SN.exe, passing it the -tp switch and the file that contains just the public key.

```
SN -tp MyCompany.PublicKey
```

When I execute this, I get the following output.

```
Microsoft (R) .NET Framework Name Utility Version 4.0.30319.17929
Copyright (c) Microsoft Corporation. All rights reserved.
```

Public key (hash algorithm: sha256):
00240000080000022000009400000000025431410000001001039fd962b61702111
850be45339b2d6a5c82b7b704755638047c6ffa37397b66291a5afb3d814a6f294010
b233ba0c0b8c098a809b8a55d425d96a4c0d0f716463d93d8651a484a6231728cac8936a26550
69f12155c319236117d602ae6c900d3685833de583fc7b81fc8b17936a567cad608ae672b6
1f8fb0b0

Public token is 3db32f3c8b42c9a

The SN utility doesn't offer any way for you to display the private key.

The size of public keys makes them difficult to work with. To make things easier for the developer
(and for end users), put public tokens are created. A public token is a 64-bit hash of the pub-
lic key. SN.exe's -tp switch shows the public key token that corresponds to the complete public key
at the end of its output.

Now how to create a public/private key pair, creating a strongly named assembly
simple. When you compile your assembly, use the /keyfile:<file> compiler switch.

```
csc /keyfile:MyCompany.snk Program.cs
```

When the C# compiler sees this, the compiler opens the specified file (MyCompany.snk),
signs the assembly with the private key, and embeds the public key in the manifest. Note that you sign
only the assembly file that contains the manifest; the other's files cannot be signed.

If you are using Visual Studio, you can create a public/private key by displaying the prop-
erties for your project, clicking the Signing tab, selecting the Sign Assembly check box, and then
choosing the <New.../> option from the Strong Name Key box

> In this example, I am using Enhanced Signing, which was introduced in .NET Framework 4.5. If you need to
produce an assembly that is compatible with previous versions of the .NET Framework, you will also have to create
a counter-signature by using the AssemblyKeyAttribute. For details about this, see: mdn.microsoft.com/
en-us/library/hh451055(v=10).assembly.