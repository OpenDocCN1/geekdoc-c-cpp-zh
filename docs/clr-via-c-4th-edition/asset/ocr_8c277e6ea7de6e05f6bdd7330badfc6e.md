Public key numbers are very big. If you want to, after creating the file that contains the public and private key, you can use the SN.exe utility again to see the actual public key. To do this, you must execute the SN.exe utility twice. First, you invoke SN.exe with the –p switch to create a file that contains only the public key (MyCompany.PublicKey).<sup>1</sup>

```
```
SN –p MyCompany.snk MyCompany.PublicKey sha256
```
```

Then, you invoke SN.exe, passing it the –tp switch and the file that contains just the public key.

```
```
SN –tp MyCompany.PublicKey
```
```

When I execute this line, I get the following output.

```
```
Microsoft (R) .NET Framework Strong Name Utility  Version 4.0.30319.17929
Copyright (c) Microsoft Corporation.  All rights reserved.

Public key (hash algorithm: sha256):
00240000048000009400000006020000002400005253413100040000010001003f9d621b702111
85b0453b92bdcba8c02e0b7b4f05d67ab02047fc786ffa3797b669215afd0b4f8a4f6f294010
b233bac0b8c809b8a09855da256d964c0d07f1f64d91d98b51a4846a62317328cac89362a550
69f2a1a25bc03193b261176dd629eace6c90d36858de3fcb781bfc8b17936a567cad608ae672b6
1fb80e0b0

Public key token is 3db32f38c8b42c9a
```
```

The SN.exe utility doesn’t offer any way for you to display the private key.

The size of public keys makes them difficult to work with. To make things easier for the developer (and for end users too), *public key tokens* were created. A public key token is a 64-bit hash of the public key. SN.exe’s –tp switch shows the public key token that corresponds to the complete public key at the end of its output.

Now that you know how to create a public/private key pair, creating a strongly named assembly is simple. When you compile your assembly, you use the `/keyfile:<file>` compiler switch.

```
```
csc /keyfile:MyCompany.snk Program.cs
```
```

When the C# compiler sees this switch, the compiler opens the specified file (MyCompany.snk), signs the assembly with the private key, and embeds the public key in the manifest. Note that you sign only the assembly file that contains the manifest; the assembly’s other files can’t be signed explicitly.

If you are using Visual Studio, you can create a new public/private key file by displaying the properties for your project, clicking the Signing tab, selecting the Sign The Assembly check box, and then choosing the `<New...>` option from the Choose A Strong Name Key File combo box.

<sup>1</sup> In this example, I am using Enhanced Strong Naming, which was introduced in .NET Framework 4.5. If you need to produce an assembly that is compatible with previous versions of the .NET Framework, then you will also have to create a counter-signature by using the AssemblySignatureKeyAttribute. For details about this, see http://msdn.microsoft.com/en-us/library/hh415055(v=vs.110).aspx.