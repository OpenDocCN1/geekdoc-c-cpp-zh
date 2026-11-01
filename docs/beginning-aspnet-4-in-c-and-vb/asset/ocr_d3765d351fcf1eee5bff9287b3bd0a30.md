+   - FileDialogPermission controls the ability to access files that have been selected by the user in the Open dialog box. This permission is commonly used when FileIOPermission is not granted to allow limited access to files.
+   - FileIOPermission controls the ability to work with files (reading, writing, and appending to files, as well as creating, altering, and accessing folders).
+   - IsolatedStorageFilePermission controls the ability to access private virtual file systems.
+   - IsolatedStoragePermission controls the ability to access isolated storage; storage that is associated with an individual user and with some aspect of the code's identity. Isolated storage is discussed in Chapter 29, "Manipulating Files and the Registry."
+   - MessageQueuePermission controls the ability to use message queues through the Microsoft Message Queue.
+   - PerformanceCounterPermission controls the ability to make use of performance counters.
+   - PrintingPermission controls the ability to print.
+   - ReflectionPermission controls the ability to discover information about a type at runtime by using System.Reflection.
+   - RegistryPermission controls the ability to read, write, create, or delete registry keys and values.
+   - SecurityPermission controls the ability to execute, assert permissions, call into unmanaged code, skip verification, and other rights.
+   - ServiceControllerPermission controls the ability to control Windows services.
+   - SocketPermission controls the ability to make or accept TCP/IP connections on a network transport address.
+   - SQLClientPermission controls the ability to access SQL Server databases with the .NET data provider for SQL Server.
+   - UIPermission controls the ability to access the user interface.
+   - WebPermission controls the ability to make or accept connections to or from the Web.

With each of these permission classes, it is often possible to specify an even deeper level of granularity; for example, the DirectoryServicesPermission allows you to differentiate between read and write access, and it also allows you to define which entries in the directory services are allowed or denied access.

# Permission Sets

Permission sets are collections of permissions. With permission sets, it is not necessary to apply every single permission to code; permissions are grouped into permission sets. For example, an assembly that has FullTrust permissions has full access to all resources. With intranet permissions, the assembly is restricted; that is, it is not allowed to write to the file system other than using the isolated storage. You can create a custom permission set that includes required permissions.

By assigning the permission to code groups, there is no need to deal with every single permission. Instead, the permissions are applied in blocks, which is why .NET has the concept of permission sets. These are lists of code access permissions grouped into a named set. The following list explains the seven named permission sets you get out of the box:

+   - FullTrust means no permission restrictions.
+   - SkipVerification means that verification is not done.
+   - Execution grants the ability to run, but not to access, any protected resources.
+   - Nothing grants no permissions and prevents the code from executing.
+   - LocalIntranet specifies a subset of the full set of permissions. For example, file IO is restricted to read access on the share where the assembly originates. With .NET 3.5 and earlier editions (before .NET 3.5 SP1) this permission set was used when an application was running from a network share.