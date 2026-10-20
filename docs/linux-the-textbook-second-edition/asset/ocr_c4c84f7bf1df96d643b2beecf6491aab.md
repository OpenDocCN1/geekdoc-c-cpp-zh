```
$ chmod 4710 cp.new
$ ls -l cp.new
-rwS--x--- 1 sarwar faculty 14 Aug 4 23:26 cp.new
$ chmod u-s cp.new
$ ls -l cp.new
-rw--x--- 1 sarwar faculty 14 Aug 4 23:26 cp.new
$ chmod u+s cp.new
$ ls -l cp.new
-rwS--x--- 1 sarwar faculty 14 Aug 4 23:26 cp.new
```

Although the idea of the SUID bit is sound, it can compromise the security of the system if not implemented correctly. For example, if the permissions of any SUID program are set to allow write privileges to others, you can change the program in this file or overwrite the existing program with another program. Doing so would allow you to execute your (new) program with superuser privileges.

# 5.6.2 SGID Bit

The SGID bit works in the same manner in which the SUID bit does, but it causes the access permissions of the process to take the group identity of the group to which the owner of the file belongs. This feature is not as dangerous as the SGID feature, because most privileged operations require superuser identity, regardless of the current group ID. The SGID bit is enabled if the execute bit for the group is displayed as s (or S) by the ls -l command. If both SGID and execute bits are enabled, the bit is displayed as s in the output of the ls -l command. If SGID bit is enabled but the execute bit is disabled, the bit is displayed as S by the ls -l command. The following session shows an example of each case.

```
$ ls -l cp.new foo
-rw-r--r-- 1 sarwar faculty 14 Aug 4 23:38 cp.new
-r-xr-sr-x 1 sarwar faculty 30 Aug 5 05:27 foo
```

+   Syntax:
+   chmod 2xxx file-list
+   chmod g+s file-list
+   Purpose: Change/set the SGID bit for files in file-list

```
$ chmod 2751 cp.new
$ ls -l cp.new
-rwxr-s--x 1 sarwar faculty 14 Aug 4 23:26 cp.new
```

```
$ chmod g+s cp.new
$ ls -l cp.new
-rwxr-S--x 1 sarwar faculty 14 Aug 4 23:26 cp.new
```

```
$ chmod g-x cp.new
$ ls -l cp.new
-rwxr---x 1 sarwar faculty 14 Aug 4 23:26 cp.new
```

```
$ chmod g+s cp.new
$ ls -l cp.new
-rwxr-S--x 1 sarwar faculty 14 Aug 4 23:26 cp.new
```