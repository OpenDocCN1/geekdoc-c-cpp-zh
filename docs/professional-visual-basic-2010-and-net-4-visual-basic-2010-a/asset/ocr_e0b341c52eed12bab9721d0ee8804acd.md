To limit your Internet applications’ access to the local file system, you create a permission set that limits that access and associates the Internet application group with this permission set. By default, the .NET environment provides one code group named All Code that is associated with the FullTrust permission set.

A permission set is a combination of security configurations. This set defines what each authorized user has access to and what that user can do on that machine — for instance, whether the user can read environment variables or the file system, or execute other code.

Security that is used within the programming environment also makes use of permission sets. Through code you can control access to files in a file system, environment variables, file dialogs, isolated storage, reflections, registry, sockets, and UI. Isolated storage and virtual file systems are new operating system–level storage locations that can be used by programs and are governed by the machine security policies. These file systems keep a machine safe from file system intrusion by designating a regulated area for file storage. The main access to these items is controlled through code access permissions.

Although many methods that we use in Visual Basic provide an identifiable return value, the only time we get a return value from security methods is when the method fails. When a security method succeeds, it does not provide a return value. If it fails, then it returns an exception object reflecting the specific error that occurred.

# PERMISSIONS IN THE SYSTEM.SECURITY.PERMISSIONS NAMESPACE

The System.Security.Permissions namespace is the namespace used in code to establish and use permissions associated with objects, including the file system, environment variables, and the registry. The namespace controls access to both operating system–level objects as well as code objects. In order to use this namespace in your project, you need to import it. Using this namespace gives you access to the CodeAccessPermission and PrincipalPermission classes for using role-based permissions and information supplied by identity permissions. CodeAccessPermission controls access to the operating system–level objects. Role-based permissions and identity permissions grant access to objects based on the identity of the user of the program that is running (the user context).

Table 32-2 lists the members of the System.Security.Permissions namespace that apply to Windows application programming. While there is a description accompanying each member, those classes that end with Attribute, such as EnvironmentPermissionAttribute, are classes that enable you to modify the security level at which your code is allowed to interact with each respective object. These objects create a declarative model for setting security that can be leveraged across multiple different implementation models.

The default environment will provide a given level of access. It is not possible to grant access beyond this level via code access security; however, when working with these classes you can specify exactly what should or should not be available in a given situation. Additionally, these classes have been marked to prevent inheritance. It really wouldn’t be a very secure system if you could inherit from one of these classes. Code could be written to override the associated security methods and grant unlimited permissions.

Table 32-2 also deals with security in regard to software publishers. A software publisher is a specific entity that is using a digital signature to identify itself in a Web-based scenario.

TABLE 32-2: Members of System.Security.Permissions

| CLASS | DESCRIPTION |
|---|---|
| CodeAccessSecurityAttribute | Base class for code access security attribute classes |
| DataProtectionPermission | Controls access to the data protection APIs, T |
| DataProtectionPermissionAttribute | Allows declarative control of DataProtectionPermssion via code |
| EnvironmentPermission | Controls the capability to see and modify system and user environment variables |