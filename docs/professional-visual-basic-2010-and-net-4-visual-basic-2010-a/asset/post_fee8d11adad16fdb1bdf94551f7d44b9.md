
# 32

# Security in the .NET Framework

# WHAT YOU WILL LEARN IN THIS CHAPTER

- Concepts and definitions
- Permissions
- Roles
- Principals
- Code access permissions
- Role-based permissions
- Identity permissions
- User Access Control (UAC)
- Encryption
- Hashing
- Symmetric Key Encryption
- Asymmetric Key Encryption
- Digital Signatures
- X.509 Certificates
- SSL

This chapter covers the basics of security and cryptography. It begins with a brief discussion of the .NET Framework’s security architecture, because this affects all the solutions you may choose to implement.

The .NET Framework provides you with best practices, tools, and core functionality with regard to security. You have the System.Security.Permissions namespace, which enables you to control code access permissions along with role-based and identity permissions. Through your code, you can control access to objects programmatically, as well as receive information on the current permissions of objects. This security framework will assist you in determining whether you have permissions to run your code, instead of getting halfway through execution and having to deal with permission-based exceptions.

Cryptography is the cornerstone of the .NET Web Services security model, so the second half of this chapter discusses the basis of cryptography and how to implement it. Specifically, it covers the following:

- Hash algorithms
- SHA
- MD5
- Secret key encryption
- Public key cryptography standard
- Digital signatures
- Certification
- Secure Sockets Layer communications

Let’s begin by looking at some security concepts and definitions.

> As always, the code for this chapter is available for download from www.wrox.com, which you may want in order to follow along.

## SECURITY CONCEPTS AND DEFINITIONS

Table 32-1 describes the different types of security presented in this chapter and how they relate to real-world scenarios.

TABLE 32-1: Types of Security

| SECURITY TYPE | RELATED CONCEPT IN SECURITY .PERMISSIONS NAMESPACE | PURPOSE |
|---|---|---|
| NTFS | None | Allows for detailed file system rights, e.g., locking down of specific files |
| Cryptographic | Strong name and assembly, generation, SignCode.exe utility | Use of public key infrastructure and certificates |
| Programmatic | Groups and permission sets | For use in pieces of code that are being called into. Provides extra security to prevent users of calling code from violating security measures implemented by the programs that are not provided for on a machine level. |
| User Access Control | Users run without administrative permission | Provided by the operating system to help users protect their system from unexpected changes that might occur when logged in using the machine’s administrator account. |

There are many approaches to providing security on the machines where your shared code is hosted. If multiple shared code applications are on one machine, each piece of shared code can be called from many front-end applications. Each piece of shared code will have its own security requirements for accessing environment variables — such as the registry, the file system, and other items — on the machine that it is running on. From an NTFS perspective, the administrator of your server can only lock down those items on the machine that are not required to be accessed from any piece of shared code running on it. Therefore, some applications need additional security built-in to prevent any calling code from doing things it is not supposed to do.

One of the more significant changes to security in .NET 4 is the removal of Code Access Security policies. Similar to the old Permview.exe, CasPol.exe is now an obsolete utility, and as such coverage of this topic has been omitted. Additionally, the PermCalc.exe tool has also been made obsolete with .NET 4.

To limit your Internet applications’ access to the local file system, you create a permission set that limits that access and associates the Internet application group with this permission set. By default, the .NET environment provides one code group named All Code that is associated with the FullTrust permission set.

A permission set is a combination of security configurations. This set defines what each authorized user has access to and what that user can do on that machine — for instance, whether the user can read environment variables or the file system, or execute other code.

Security that is used within the programming environment also makes use of permission sets. Through code you can control access to files in a file system, environment variables, file dialogs, isolated storage, reflections, registry, sockets, and UI. Isolated storage and virtual file systems are new operating system–level storage locations that can be used by programs and are governed by the machine security policies. These file systems keep a machine safe from file system intrusion by designating a regulated area for file storage. The main access to these items is controlled through code access permissions.

Although many methods that we use in Visual Basic provide an identifiable return value, the only time we get a return value from security methods is when the method fails. When a security method succeeds, it does not provide a return value. If it fails, then it returns an exception object reflecting the specific error that occurred.

## PERMISSIONS IN THE SYSTEM.SECURITY.PERMISSIONS NAMESPACE

The System.Security.Permissions namespace is the namespace used in code to establish and use permissions associated with objects, including the file system, environment variables, and the registry. The namespace controls access to both operating system–level objects as well as code objects. In order to use this namespace in your project, you need to import it. Using this namespace gives you access to the CodeAccessPermission and PrincipalPermission classes for using role-based permissions and information supplied by identity permissions. CodeAccessPermission controls access to the operating system–level objects. Role-based permissions and identity permissions grant access to objects based on the identity of the user of the program that is running (the user context).

Table 32-2 lists the members of the System.Security.Permissions namespace that apply to Windows application programming. While there is a description accompanying each member, those classes that end with Attribute, such as EnvironmentPermissionAttribute, are classes that enable you to modify the security level at which your code is allowed to interact with each respective object. These objects create a declarative model for setting security that can be leveraged across multiple different implementation models.

The default environment will provide a given level of access. It is not possible to grant access beyond this level via code access security; however, when working with these classes you can specify exactly what should or should not be available in a given situation. Additionally, these classes have been marked to prevent inheritance. It really wouldn’t be a very secure system if you could inherit from one of these classes. Code could be written to override the associated security methods and grant unlimited permissions.

Table 32-2 also deals with security in regard to software publishers. A software publisher is a specific entity that is using a digital signature to identify itself in a Web-based scenario.

TABLE 32-2: Members of System.Security.Permissions

| CLASS | DESCRIPTION |
|---|---|
| CodeAccessSecurityAttribute | Base class for code access security attribute classes |
| DataProtectionPermission | Controls access to the data protection APIs, T |
| DataProtectionPermissionAttribute | Allows declarative control of DataProtectionPermission via code |
| EnvironmentPermission | Controls the capability to see and modify system and user environment variables |
