
Comparing the symmetric keys created from Alice and Bob shows that the same key value gets created.
Using this symmetric key and the initialization vector, the message from Alice can be decrypted with the AesCryptoServiceProvider class.

```csharp
private static void BobReceivesData(byte[] encryptedData)
{
    Console.WriteLine("Bob receives encrypted data");
    byte[] rawData = null;

    var aes = new AesCryptoServiceProvider();

    int nBytes = aes.BlockSize / 8;
    byte[] iv = new byte[nBytes];
    for (int i = 0; i < iv.Length; i++)
        iv[i] = encryptedData[i];

    using (var bobAlgorithm = new ECDiffieHellmanCng(bobKey))
    using (CngKey alicePubKey = CngKey.Import(alicePubKeyBlob,
        CngKeyBlobFormat.EccPublicBlob))
    {
        byte[] symmKey = bobAlgorithm.DeriveKeyMaterial(alicePubKey);
        Console.WriteLine("Bob creates this symmetric key with " +
            "Alice's public key information: {0}",
            Convert.ToBase64String(symmKey));

        aes.Key = symmKey;
        aes.IV = iv;

        using (ICryptoTransform decryptor = aes.CreateDecryptor())
        using (MemoryStream ms = new MemoryStream())
        {
            var cs = new CryptoStream(ms, decryptor, CryptoStreamMode.Write);
            cs.Write(encryptedData, nBytes, encryptedData.Length - nBytes);
            cs.Close();

            rawData = ms.ToArray();

            Console.WriteLine("Bob decrypts message to: {0}",
                Encoding.UTF8.GetString(rawData));
        }
    }
    aes.Clear();
}
```

When you run the application, you can see output similar to the following on the console. The message from Alice is encrypted, and decrypted by Bob with the securely exchanged symmetric key.

```text
Alice sends message: secret message
Alice creates this symmetric key with Bob's public key information:
5NWat8emZFCYoIIla9SIVn4AXy4iALRATFo4iVbw=
Alice: message is encrypted: 3CSU9CpXmoPtk3Bw2V0TS P0ojg rycSR7Te8z tau5N0=

Bob receives encrypted message
Bob creates this symmetric key with Alice's public key information:
5NWat8emZFCYoIIla9SIVn4AXy4iALRATFo4iVbw=
Bob decrypts message to: secret message
```

## ACCESS CONTROL TO RESOURCES

With the operating system, resources such as files and registry keys, as well as handles of a named pipe, are secured by using an access control list. Figure 21-3 shows the structure of how this maps. The resource has a security descriptor associated. The security descriptor contains information about the owner of the resource and references two access control lists: a discretionary access control list (DACL) and a system access control list (SACL). The DACL defines who has access or no access; the SACL defines audit rules for security event logging. An ACL contains a list of access control entries (ACE). The ACE contains a type, a security identifier, and rights. With the DACL, the ACE can be of type access allowed or access denied. Some of the rights that you can set and get with a file are create, read, write, delete, modify, change permissions, and take ownership.

![](img/d7d2ffa0a76feaab821930e95daace93_620_0.png)

**FIGURE 21-3**

The classes to read and modify access control are located in the namespace System.Security.AccessControl. The following program demonstrates reading the access control list from a file.

The FileStream class defines the GetAccessControl() method, which returns a FileSecurity object. FileSecurity is the .NET class that represents a security descriptor for files. FileSecurity derives from the base classes ObjectSecurity, CommonObjectSecurity, NativeObjectSecurity, and FileSystemSecurity. Other classes that represent a security descriptor are CryptoKeySecurity, EventWaitHandleSecurity, MutexSecurity, RegistrySecurity, SemaphoreSecurity, PipeSecurity, and ActiveDirectorySecurity. All of these objects can be secured using an access control list. In general, the corresponding .NET class defines the method GetAccessControl to return the corresponding security class; for example, the Mutex.GetAccessControl() method returns a MutexSecurity, and the PipeStream.GetAccessControl() method returns a PipeSecurity.

The FileSecurity class defines methods to read and change the DACL and SACL. The method GetAccessRules() returns the DACL in the form of the class AuthorizationRuleCollection. To access the SACL, you can use the method GetAuditRules().

With the method GetAccessRules(), you can define if inherited access rules, and not only access rules directly defined with the object, should be used. The last parameter defines the type of the security identifier that should be returned. This type must derive from the base class IdentityReference. Possible types are NTAccount and SecurityIdentifier. Both of these classes represent users or groups; the NTAccount class finds the security object by its name and the SecurityIdentifier class finds the security object by a unique security identifier.

The returned AuthorizationRuleCollection contains AuthorizationRule objects. The AuthorizationRule is the .NET representation of an ACE. With the sample here, a file is accessed, so the AuthorizationRule can be cast to a FileSystemAccessRule. With ACEs of other resources, different .NET representations exist, such as MutexAccessRule and PipeAccessRule. With the FileSystemAccessRule class, the properties AccessControlType, FileSystemRights, and IdentityReference return information about the ACE.

```csharp
using System;
using System.IO;
using System.Security.AccessControl;
using System.Security.Principal;

namespace Wrox.ProCSharp.Security
{
    class Program
    {
        static void Main(string[] args)
        {
            string filename = null;
            if (args.Length == 0)
                return;

            filename = args[0];

            FileStream stream = File.Open(filename, FileMode.Open);
            FileSecurity securityDescriptor = stream.GetAccessControl();
            AuthorizationRuleCollection rules =
                securityDescriptor.GetAccessRules(true, true,
                    typeof(NTAccount));

            foreach (AuthorizationRule rule in rules)
            {
                var fileRule = rule as FileSystemAccessRule;
                Console.WriteLine("Access type: {0}", fileRule.AccessControlType);
                Console.WriteLine("Rights: {0}", fileRule.FileSystemRights);
                Console.WriteLine("Identity: {0}",
                    fileRule.IdentityReference.Value);
                Console.WriteLine();
            }
        }
    }
}
```

code snippet FileAccessControl/Program.cs

By running the application and passing a filename, you can see the access control list for the file. The output shown here lists full control to Administrators and System, modification rights to authenticated users, and read and execute rights to all users belonging to the group Users:

```text
Access type: Allow
Rights: FullControl
Identity: BUILTIN\Administrators

Access type: Allow
Rights: FullControl
Identity: NT AUTHORITY\SYSTEM

Access type: Allow
Rights: Modify, Synchronize
Identity: NT AUTHORITY\Authenticated Users

Access type: Allow
Rights: ReadAndExecute, Synchronize
Identity: BUILTIN\Users
```

Setting access rights is very similar to reading access rights. To set access rights, several resource classes that can be secured offer the SetAccessControl() and ModifyAccessControl() methods. The sample code here modifies the access control list of a file by invoking the SetAccessControl() method from the File class. To this method a FileSecurity object is passed. The FileSecurity object is filled with FileSystemAccessRule objects. The access rules listed here deny write access to the Sales group, give read access to the Everyone group, and give full control to the Developers group.

## Security Transparency Level 2

You can annotate an assembly with the attribute SecurityRules and set the SecurityRuleSet.Level2 for applying the new level with .NET 4. (This is the default with .NET 4.) For backward compatibility, set it to Level1.

```csharp
[assembly: SecurityRules(SecurityRuleSet.Level2)]
```

If you set the attribute SecurityTransparent, the complete assembly will not do anything privileged or unsafe. This assembly can only call other transparent code or safe-critical code. This attribute can be applied only to the complete assembly.

```csharp
[assembly: SecurityTransparent()]
```

The attribute AllowPartiallyTrustedCallers is somewhere between transparent and the other categories. With this attribute, the code defaults to transparent, but individual types or members can have other attributes:

```csharp
[assembly: AllowPartiallyTrustedCallers()]
```

If none of these attributes are applied, the code is security critical. However, you can apply the attribute SecuritySafeCritical to individual types and members to make them callable from transparent code:

```csharp
[assembly: SecurityCritical()]
```

## Permissions

If code runs inside a sandbox, the sandbox can define what the code is allowed to do by defining .NET permissions. While the full trust applies to applications running on the desktop, applications running in a sandbox are only allowed to do the actions that are defined by the permissions that the host is giving to the sandbox. You can also define permissions for an application domain that is started from a desktop application. This is done with the Sandbox API.

> Application domains are discussed in Chapter 18, “Assemblies.”

Permissions refer to the actions that each code group is allowed to perform (or prevented from performing). For example, permissions include “read files from the file system,” “write to the Active Directory,” and “use sockets to open network connections.” Several predefined permissions exist, but you can also create your own permissions.

.NET permissions are independent of operating system permissions. .NET permissions are just verified by the CLR. An assembly demands a permission for a specific operation (for example, the File class demands the FileIOPermission), and the CLR verifies that the assembly has the permission granted so that it can continue.

There is a very fine-grained list of permissions that you can apply to an assembly or request from code. The following list shows a few of the code access permissions provided by the CLR; as you can see, you have great control of what code is or is not permitted to do:

- DirectoryServicesPermission controls the ability to access Active Directory through the System.DirectoryServices classes.
- DnsPermission controls the ability to use the TCP/IP Domain Name System (DNS).
- EnvironmentPermission controls the ability to read and write environment variables.
- EventLogPermission controls the ability to read and write to the event log.
