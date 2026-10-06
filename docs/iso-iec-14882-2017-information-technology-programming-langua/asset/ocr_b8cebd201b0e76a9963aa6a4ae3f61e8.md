# ISO/IEC 14882:2017(E)

7 Returns: true if a new directory was created, otherwise false. The signature with argument ec returns false if an error occurs.

8 Throws: As specified in 30.10.7.

# 30.10.15 Create directory symlink

```
void create_directory_symlink(const path& to, const path& new_symlink);
void create_directory_symlink(const path& to, const path& new_symlink,
                               error_code& ec) noexcept;
```

+   1 Effects: Established the postcondition, as by POSIX symlink().

+   2 Postconditions: new_symlink resolves to a symbolic link file that contains an unspecified respect of.

+   3 Throws: As specified in 30.10.7.

+   4 [Note: Some operating systems require symlink creation to identify that the link is a directory. Portable code should use create_directory_symlink() to create directory symlinks rather than create_symlink() -- end note]

+   5 [Note: Some operating systems do not support symbolic links at all or support them only for regular files. Some file systems (such as the FAT file system) do not support symbolic links regardless of the operating system. -- end note]

# 30.10.15.9 Create hard link

```
void create_hard_link(const path& to, const path& new_hard_link);
void create_hard_link(const path& to, const path& new_hard_link,
                               error_code& ec) noexcept;
```

+   1 Effects: Established the postcondition, as by POSIX symlink().

+   2 Postconditions:

+   - exists(to) && exists(new_hard_link) && equivalent(to, new_hard_link)

+   - The contents of the file or directory are not changed.

+   3 Throws: As specified in 30.10.7.

+   4 [Note: Some operating systems do not support hard links at all or support them only for regular files. Some file systems (such as the FAT file system) do not support hard links regardless of the operating system. Some file systems limit the number of links per file. -- end note]

# 30.10.15.10 Create symlink

```
void create_symlink(const path& to, const path& new_symlink);
void create_symlink(const path& to, const path& new_symlink,
                               error_code& ec) noexcept;
```

+   1 Effects: Established the postcondition, as by POSIX symlink().

+   2 Postconditions: new_symlink resolves to a symbolic link file that contains an unspecified respect of.

+   3 Throws: As specified in 30.10.7.

+   4 [Note: Some operating systems do not support symbolic links at all or support them only for regular files. Some file systems (such as the FAT file system) do not support symbolic links regardless of the operating system. -- end note]