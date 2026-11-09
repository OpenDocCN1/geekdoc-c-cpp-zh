
## Delayed Signing

Earlier in this chapter, I discussed how the SN.exe tool can produce public/private key pairs. This tool generates the keys by making calls into the Crypto API provided by Windows. These keys can be stored in files or other storage devices. For example, large organizations (such as Microsoft) will maintain the returned private key in a hardware device that stays locked in a vault; only a few people in the company have access to the private key. This precaution prevents the private key from being compromised and ensures the key's integrity. The public key is, well, public and freely distributed.

When you're ready to package your strongly named assembly, you'll have to use the secure private key to sign it. However, while developing and testing your assembly, gaining access to the secure private key can be a hassle. For this reason, the .NET Framework supports *delayed signing*, sometimes referred to as *partial signing*. Delayed signing allows you to build an assembly by using only your company's public key; the private key isn't necessary. Using the public key allows assemblies that reference your assembly to embed the correct public key value in their AssemblyRef metadata entries. It also allows the assembly to be placed in the GAC appropriately. If you don't sign the file with your company's private key, you lose all of the tampering protection afforded to you because the assembly's files won't be hashed, and a digital signature won't be embedded in the file. This loss of protection shouldn't be a problem, however, because you use delayed signing only while developing your own assembly, not when you're ready to package and deploy the assembly.

Basically, you get your company's public key value in a file and pass the file name to whatever utility you use to build the assembly. (As I have shown earlier in this chapter, you can use SN.exe's **-p** switch to extract a public key from a file that contains a public/private key pair.) You must also tell the tool that you want the assembly to be delay signed, meaning that you're not supplying a private key. For the C# compiler, you do this by specifying the **/delaysign** compiler switch. In Visual Studio, you display the properties for your project, click the Signing tab, and then select the Delay Sign Only check box. If you're using AL.exe, you can specify the **/delay[+|-]sign** command-line switch.

When the compiler or AL.exe detects that you're delay signing an assembly, it will emit the assembly's AssemblyDef manifest entry, which will contain the assembly's public key. Again, the presence of the public key allows the assembly to be placed in the GAC. It also allows you to build other assemblies that reference this assembly; the referencing assemblies will have the correct public key in their AssemblyRef metadata table entries. When creating the resulting assembly, space is left in the resulting PE file for the RSA digital signature. (The utility can determine how much space is necessary from the size of the public key.) Note that the file's contents won't be hashed at this time either.

At this point, the resulting assembly doesn't have a valid signature. Attempting to install the assembly into the GAC will fail because a hash of the file's contents hasn't been done—the file appears to have been tampered with. On every machine on which the assembly needs to be installed into the GAC, you must prevent the system from verifying the integrity of the assembly's files. To do this, you use the SN.exe utility, specifying the **-Vr** command-line switch. Executing SN.exe with this switch also tells the CLR to skip checking hash values for any of the assembly's files when loaded at runtime.

Internally, SN’s –Vr switch adds the assembly’s identity under the following registry subkey:
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\StrongNameVerification.

**Important** When using a utility that manipulates the registry, make sure that you run the 64-bit version of the utility on a 64-bit machine. By default, the 32-bit utilities are installed in C:\Program Files (x86)\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools, and the 64-bit utilities are installed in C:\Program Files (x86)\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools\x64.

When you’re finished developing and testing the assembly, you need to officially sign it so that you can package and deploy it. To sign the assembly, use the SN.exe utility again, this time with the –R switch and the name of the file that contains the actual private key. The –R switch causes SN.exe to hash the file’s contents, sign it with the private key, and embed the RSA digital signature in the file where the space for it had previously been reserved. After this step you can deploy the fully signed assembly. On the developing and testing machines, don’t forget to turn verification of this assembly back on by using SN.exe’s –Vu or –Vx command-line switch. The following list summarizes the steps discussed in this section to develop your assembly by using the delayed signing technique:

- 1. While developing an assembly, obtain a file that contains only your company’s public key, and compile your assembly by using the /keyfile and /delaysign compiler switches:
    ```
    csc /keyfile:MyCompany.PublicKey /delaysign MyAssembly.cs
    ```
- 2. After building the assembly, execute the following line so that the CLR will trust the assembly’s bytes without performing the hash and comparison. This allows you to install the assembly in the GAC (if you desire). Now, you can build other assemblies that reference the assembly, and you can test the assembly. Note that you have to execute the following command line only once per machine; it’s not necessary to perform this step each time you build your assembly.
    ```
    SN.exe –Vr MyAssembly.dll
    ```
- 3. When ready to package and deploy the assembly, obtain your company’s private key, and then execute the line below. You can install this new version in the GAC if you desire, but don’t attempt to install it in the GAC until executing step 4.
    ```
    SN.exe –Ra MyAssembly.dll MyCompany.PrivateKey
    ```
- 4. To test in real conditions, turn verification back on by executing the following command line:
    ```
    SN.exe –Vu MyAssembly.dll
    ```

At the beginning of this section, I mentioned how organizations keep their key pairs in a hardware device such as a smart card. To keep these keys secure, you must make sure that the key values are never persisted in a disk file. Cryptographic service providers (CSPs) offer containers that abstract the location of the keys. Microsoft, for example, uses a CSP that has a container that, when accessed, obtains the private key from a hardware device.

If your public/private key pair is in a CSP container, you’ll have to specify different switches to the CSC.exe, AL.exe, and SN.exe programs: When compiling (CSC.exe), specify the /keycontainer switch instead of the /keyfile switch; when linking (AL.exe), specify its /keyname switch instead of its /keyfile switch; and when using the Strong Name program (SN.exe) to add a private key to a delay-signed assembly, specify the –Rc switch instead of the –R switch. SN.exe offers additional switches that allow you to perform operations with a CSP.

**Important** Delayed signing is also useful whenever you want to perform some other operation to an assembly before you package it. For example, you may want to run an obfuscator over your assembly. You can’t obfuscate an assembly after it’s been fully signed because the hash value will be incorrect. So, if you want to obfuscate an assembly file or perform any other type of post-build operation, you should use delayed signing, perform the post-build operation, and then run SN.exe with the –R or –Rc switch to complete the signing process of the assembly with all of its hashing.

### Privately Deploying Strongly Named Assemblies

Installing assemblies into the GAC offers several benefits. The GAC enables many applications to share assemblies, reducing physical memory usage on the whole. In addition, it’s easy to deploy a new version of the assembly into the GAC and have all applications use the new version via a publisher policy (described later in this chapter). The GAC also provides side-by-side management for an assembly’s different versions. However, the GAC is usually secured so that only an administrator can install an assembly into it. Also, installing into the GAC breaks the simple copy deployment story.

Although strongly named assemblies can be installed into the GAC, they certainly don’t have to be. In fact, it’s recommended that you deploy assemblies into the GAC only if the assembly is intended to be shared by many applications. If an assembly isn’t intended to be shared, it should be deployed privately. Deploying privately preserves the simple copy install deployment story and better isolates the application and its assemblies. Also, the GAC isn’t intended to be the new C:\Windows\System32 dumping ground for common files. The reason is because new versions of assemblies don’t overwrite each other; they are installed side by side, eating up disk space.

In addition to deploying a strongly named assembly in the GAC or privately, a strongly named assembly can be deployed to some arbitrary directory that a small set of applications know about. For example, you might be producing three applications, all of which want to share a strongly named assembly. Upon installation, you can create four directories: one for each application and an additional directory for the assembly you want shared. When you install each application into its directory, also install an XML configuration file, and have the shared assembly’s codeBase element indicate the path of the shared assembly. Now at runtime, the CLR will know to look in the strongly named assembly’s directory for the shared assembly. For the record, this technique is rarely used and is somewhat discouraged because no single application controls when the assembly’s files should be uninstalled.

**Note** The configuration file’s codeBase element actually identifies a URL. This URL can refer to any
