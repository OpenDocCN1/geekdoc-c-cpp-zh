The following list summarizes the steps discussed in this section to develop your assembly by using the delayed signing technique:

+   1. While developing an assembly, obtain a file that contains only your company’s public key, and compile your assembly by using the `/keyfile` and `/delaysign` compiler switches.

```
csc /keyfile:MyCompany.PublicKey /delaysign MyAssembly.cs
```

+   2. After building the assembly, execute the following line so that the CLR will trust the assembly’s bytes without performing the hash and comparison. This allows you to install the assembly in the GAC (if you desire). Now, you can build other assemblies that reference the assembly, and you can test the assembly. Note that you have to execute the following command line only once per machine; it’s not necessary to perform this step each time you build your assembly.

```
SN.exe -Vr MyAssembly.dll
```

+   3. When ready to package and deploy the assembly, obtain your company’s private key, and then execute the following line. You can install this new version in the GAC if you desire, but don’t attempt to install it in the GAC until executing step 4.

```
SN.exe -Ra MyAssembly.dll MyCompany.PrivateKey
```

+   4. To test in real conditions, turn verification back on by executing the following command line.

```
SN.exe -Vu MyAssembly.dll
```

At the beginning of this section, I mentioned how organizations keep their key pairs in a hardware device such as a smart card. To keep these keys secure, you must make sure that the key values are never persisted in a disk file. Cryptographic service providers (CSPs) offer containers that abstract the location of these keys. Microsoft, for example, uses a CSP that has a container that, when accessed, obtains the private key from a hardware device.

If your public/private key pair is in a CSP container, you’ll have to specify different switches to the CSC.exe, AL.exe, and SN.exe programs: When compiling (CSC.exe), specify the `/keycontainer` switch instead of the `/keyfile` switch; when linking (AL.exe), specify its `/keyname` switch instead of its `/keyfile` switch; and when using the Strong Name program (SN.exe) to add a private key to a delay-signed assembly, specify the `-Rc` switch instead of the `-R` switch. SN.exe offers additional switches that allow you to perform operations with a CSP.

> > **Important** Delayed signing is also useful whenever you want to perform some other operation to an assembly before you package it. For example, you may want to run an obfuscator over your assembly. You can’t obfuscate an assembly after it’s been fully signed because the hash value will be incorrect. So, if you want to obfuscate an assembly file or perform any other type of post-build operation, you should use delayed signing, perform the post-build operation, and then run SN.exe with the `-R` or `-Rc` switch to complete the signing process of the assembly with all of its hashing.