tells the CLR to skip checking hash values for any of the assembly’s files when loaded at runtime.

Internally, SN’s –Vr switch adds the assembly’s identity under the following registry subkey:
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\StrongNameVerification.

**Important** When using an utility that manipulates the registry, make sure that you run the 64-bit version of the utility on a 64-bit machine. By default, the 32-bit utilities are installed in C:\Program Files (x86)\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools, and the 64-bit utilities are installed in C:\Program Files (x86)\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools\x64.

When you’re finished developing and testing the assembly, you need to officially sign it so that you can package and deploy it. To sign the assembly, use the SN.exe utility again, this time with the –R switch and the name of the file that contains the actual private key. The –R switch causes SN.exe to hash the file’s contents, sign it with the private key, and embed the RSA digital signature in the file where the space for it had previously been reserved. After this step you can deploy the fully signed assembly. On the developing and testing machines, don’t forget to turn verification of this assembly back on by using SN.exe’s –Vu or –Vx command-line switch. The following list summarizes the steps discussed in this section to develop your assembly by using the delayed signing technique:

+   1. While developing an assembly, obtain a file that contains only your company’s public key, and compile your assembly by using the /keyfile and /delaysign compiler switches:

```
csc /keyfile:MyCompany.PublicKey /delaysign MyAssembly.cs
```

+   2. After building the assembly, execute the following line so that the CLR will trust the assembly’s bytes without performing the hash and comparison. This allows you to install the assembly in the GAC (if you desire). Now, you can build other assemblies that reference the assembly, and you can test the assembly. Note that you have to execute the following command line only once per machine; it’s not necessary to perform this step each time you build your assembly.

```
SN.exe –Vr MyAssembly.dll
```

+   3. When ready to package and deploy the assembly, obtain your company’s private key, and then execute the line below. You can install this new version in the GAC if you desire, but don’t attempt to install it in the GAC until executing step 4.

```
SN.exe –Ra MyAssembly.dll MyCompany.PrivateKey
```

+   4. To test in real conditions, turn verification back on by executing the following command line:

```
SN.exe –Vu MyAssembly.dll
```

At the beginning of this section, I mentioned how organizations keep their key pairs in a hardware device such as a smart card. To keep these keys secure, you must make sure that the key values are never persisted in a disk file. Cryptographic service providers (CSPs) offer containers that abstract the location of the keys. Microsoft, for example, uses a CSP that has a container that, when accessed, obtains the private key from a hardware device.