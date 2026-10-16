System.IO.FileSystem

System.IO.FileSystem.AccessControl

# Namespaces

System.IO

System.Security.AccessControl

System.Security.Principal

static System.Console

The FileStream class defines the GetAccessControl method, which returns a FileSecurity object. FileSecurity is the .NET class that represents a security descriptor for files. FileSecurity derives from the base classes ObjectSecurity, CommonObjectSecurity, NativeObjectSecurity, and FileSystemSecurity. Other classes that represent a security descriptor are CryptoKeySecurity, EventWaitHandleSecurity, MutexSecurity, RegistrySecurity, SemaphoreSecurity, PipeSecurity, and ActiveDirectorySecurity. All of these objects can be secured using an ACL. In general, the corresponding .NET class defines the method GetAccessControl to return the corresponding security class; for example, the Mutex.GetAccessControl method returns a MutexSecurity, and the PipeStream.GetAccessControl method returns a PipeSecurity.

The FileSecurity class defines methods to read and change the DACL and SACL. The method GetAccessRules returns the DACL in the form of the class AuthorizationRuleCollection. To access the SACL, you can use the method GetAuditRules.

With the method GetAccessRules, you can specify whether inherited access rules, and not only access rules directly defined with the object, should be used. The last parameter defines the type of the security identifier that should be returned. This type must derive from the base class IdentityReference. Possible types are NTAccount and SecurityIdentifier. Both of these classes represent users or groups; the NTAccount class finds the security object by its name and the SecurityIdentifier class finds the security object by a unique security identifier.

The returned AuthorizationRuleCollection contains AuthorizationRule objects. The AuthorizationRule is the .NET representation of an ACE. In the following example, a file is accessed, so the AuthorizationRule can be cast to a FileSystemAccessRule. With ACEs of other resources, different .NET representations exist, such as MutexAccessRule and PipeAccessRule. With the FileSystemAccessRule class, the properties AccessControlType, FileSystemRights, and IdentityReference return information about the ACE (code file FileAccessControl/Program.cs).

```
class Program
{
```