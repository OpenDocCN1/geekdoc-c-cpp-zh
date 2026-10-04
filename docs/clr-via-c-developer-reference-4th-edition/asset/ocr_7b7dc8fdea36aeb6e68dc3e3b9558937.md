# Important Because public keys are such large numbers, and a single assembly might reference many assemblies, a large percentage of the resulting file's total size would be occupied with public key information. To conserve storage space, Microsoft hashes the public key and takes the last 8 bytes of the hashed value. These reduced public key values—known as public tokens—are actually stored in an AssemblyRef table. In general, developers and end users will use public key tokens much more frequently than full public keys.

Note, however, that the CLR never uses public tokens when making security or trust decisions because it is possible that several public keys could hash to a single public token.

The AssemblyRef metadata information (obtained by using ILDasm.exe) for a simple class library file is shown here.

```
AssemblyRef #1 (230000001)
----------------------------
Token: 0x23000001
Public Key or Token: b7 7a 5c 56 19 34 e0 89
Name: mscorlib
Version: 4.0.0.0
Major Version: 0x00000004
Minor Version: 0x00000000
Build Number: 0x00000000
Revision Number: 0x00000000
Locale: <null>
HashValue Blob:
Flags: [none] (00000000)
```

From this, you can see that the DLL assembly references a type that is contained in an assembly matching the following attributes.:

"MSCorLib,Version-4.0.0.0, Culture=neutral, PublicKey=b77a5c561934e089"

Unfortunately, ILDasm.exe uses the term Locale when it really should be using Culture.

If you look at the DLL assembly's AssemblyDef metadata table, you will see the following.

# Assembly

```
Token: 0x20000001
Name : SomeClassLibrary
Public Key :
Hash Algorithm : 0x00000804
Version: 3.0.0.0
Major Version: 0x00000003
Minor Version: 0x00000000
Build Number: 0x00000000
Revision Number: 0x00000000
Locale: <null>
Flags : [none] (00000000)
```