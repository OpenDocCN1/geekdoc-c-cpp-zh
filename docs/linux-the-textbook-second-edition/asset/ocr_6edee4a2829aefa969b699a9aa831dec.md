# Exercise 17.42

Give other examples of DAC, MAC, and RBAC.

On the command line, an ordinary user or the system administrator is able to implement resource use restrictions and privileges by controlling process credential assignments, exercised on subject executable image files, via the chmod command. On Linux, an ordinary unprivileged user can be given the required privileged role with the su or sudo command. Then, as root, she can issue a privileged chmod, chown, and chgrp to grant or modify file and directory access permissions, and use the DAC, MAC, or RBAC methods.

# Types of Credentials

We are concerned with the three basic types of credentials that the Linux kernel supports. These are as follows, with major references in the text shown:

Traditional UNIX Credentials—See Chapter 5 for a more complete exposition of these.

+   1. Real UID
+   2. Real GID

UID and GID are assigned to most Linux objects. These in large part define the object context of that object, with processes included in this assignment.

+   3. Effective (EUID), Saved (SUID), and File System (FSID) UID
+   4. Effective (EGID), Saved (SGID), and (FSGID) GID
+   5. Supplementary groups

The additional credentials used by processes are EUID/EGID/GROUPS, and are used as the subject context, and real UID/GID will be used as the object context.

# Access Control Lists

ACLs provide the ordinary, unprivileged user with the ability to set finer access controls on directories and files than the traditional Linux permissions, whether they are used on ext4 or ZFS file systems. Two different basic types of ACL apply to files and directories. An ACL that defines the current access permissions of files and directories is called an access ACL. An ACL, which can only logically be set on a directory, and that defines the permissions that a directory object inherits from its parent directory at the time of its creation, is called a default ACL. Additional basic types of ACL are minimal and extended ACLs. ACL permissions that can be equivalent to the traditional file mode permissions are called minimal ACLs. Minimal ACLs have three entries, which can be the same as the traditional file permissions. ACLs with more than three entries are called extended ACLs. Extended ACLs also contain a mask entry and may contain any number of named user and named group entries.

See Chapter W26, Section 9.3 and its subsections, at the book website, for more information about POSIX.1e and NFSV4 ACL’s.

Capabilities—See the man page for capabilities on your system

+   1. Set of permitted capabilities
+   2. Set of inheritable capabilities
+   3. Set of effective capabilities
+   4. Capability bounding set

These are most pertinent when they apply to processes, which are the active elements in system operation. They are privileged permissions exercised in a “finer-grained” context. Finer-grained is used here to mean a more specific, targeted privilege. These are applied to a process or processes that ordinarily,