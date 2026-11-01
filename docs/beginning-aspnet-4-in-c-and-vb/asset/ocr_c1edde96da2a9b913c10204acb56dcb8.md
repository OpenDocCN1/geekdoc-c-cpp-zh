Next, the file's ACL is listed again. The following is an example of what the preceding code could produce:

```
Provide full file path: C:\Users\Bill\Sample.txt
ACL list before modification:
C:\Sample.txt provides FullControl access for NT AUTHORITY\SYSTEM
C:\Sample.txt provides FullControl access for BUILTIN\Administrators
C:\Sample.txt provides FullControl access for PUSHKIN\Bill

ACL list after modification:
C:\Sample.txt provides FullControl access for PUSHKIN\Fuija
C:\Sample.txt provides FullControl access for NT AUTHORITY\SYSTEM
C:\Sample.txt provides FullControl access for BUILTIN\Administrators
C:\Sample.txt provides FullControl access for PUSHKIN\Bill
```

To remove a rule from the ACL list, there is really not much that needs to be done to the code. From the previous code example, you simply need to change the line

```
fileSec.AddAccessRule(newRule);
```

to the following to remove the rule that was just added:

```
fileSec.RemoveAccessRule(newRule);
```

# READING AND WRITING TO THE REGISTRY

In all versions of Windows since Windows 95, the registry has been the central repository for all configuration information relating to Windows setup, user preferences, and installed software and devices. Almost all commercial software these days uses the registry to store information about itself, and COM components must place information about themselves in the registry in order to be called by clients. The .NET Framework and its accompanying concept of zero-impact installation has slightly reduced the significance of the registry for applications in the sense that assemblies are entirely self-contained; no information about particular assemblies needs to be placed in the registry, even for shared assemblies. In addition, the .NET Framework has brought the concept of isolated storage — applications can store information that is particular to each user in files — and .NET Framework ensures that data is stored separately for each user registered on a machine.

The fact that applications can now be installed using the Windows Installer also frees developers from some of the direct manipulation of the registry that used to be involved in installing applications. However, despite this, the possibility exists that if you distribute any complete application, your application will use the registry to store information about its configuration. For instance, if you want your application to show up in the Add/Remove Programs dialog box in the Control Panel, this will involve appropriate registry entries. You may also need to use the registry for backward compatibility with legacy code.

As you would expect from a library as comprehensive as the .NET library, it includes classes that give you access to the registry. Two classes are concerned with the registry, and both are in the Microsoft.Win32 namespace. The classes are Registry and RegistryKey. Before you examine these classes, the following section briefly reviews the structure of the registry itself.

# The Registry

The registry has a hierarchical structure much like that of the file system. The usual way to view or modify the contents of the registry is with one of two utilities: regedit or regedt32. Of these, regedit comes with all versions of Windows since Windows 95, regedt32 comes with Windows NT and Windows 2000; it is less user-friendly than regedit, but allows access to security information that regedit is unable to view. Windows Server 2003 has merged regedit and regedt32 into a single new editor simply called regedit. For the discussion here, you will use regedit from Windows 7, which you can launch by typing regedit in the Run dialog or at the command prompt.

Figure 29-16 shows what you get when you launch regedit for the first time.