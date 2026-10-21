```
std::filesystem::rename("tmp/sub/x", "tmp/x");  // OK
```

last_write_time() uses the timepoint format as described in section “Dealing with the Last Modification”. For example:

```
// touch file p (update last file access):
std::filesystem::last_write_time(p,
    std::filesystem::file_time_type::clock::now());
```

permissions() uses the permission API format as described in section “Permissions”. The optional mode is of the bitmap enumeration type perm_options, defined in namespace std::filesystem. On the one hand, it allows you to choose between replace, add, and remove. On the other hand, using nofollow it allows you to modify permissions of the symbolic links instead of the files they refer to.
For example:

```
// remove write access for group and any access for others:
permissions(mypath,
    std::filesystem::perms::group_write
  | std::filesystem::perms::others_all,
    std::filesystem::perm_options::remove);
```

Note again that Windows supports different permission concepts. Its ACL permission concept supports only two modes:

+   - Read, write, and execute/search for all (rwxrwxrwx)
+   - Read and execute/search for all (r-xr-xr-x)

To switch portably between these two modes, you have to enable or disable all three write flags together (removing one after the other does not work):

```
// portable value to enable/disable write access:
auto allWrite = std::filesystem::perms::owner_write
  | std::filesystem::perms::group_write
  | std::filesystem::perms::others_write;
// portably remove write access:
permissions(file, allWrite, std::filesystem::perm_options::remove);
```

A shorter (but maybe less readable) way to initialize allWrite (using relaxed enum initialization) would be as follows:

```
std::filesystem::perms allWrite{0222};
```

resize_file() can be used to reduce or extend the size of a regular file: For example:

```
// make file empty:
resize_file(file, 0);
```

# 20.4.5 Symbolic Links and Filesystem-Dependent Path Conversions

Table Filesystem Path Conversions lists the operations for dealing with the path of files that take the filesystem into account. This is especially important if you have to deal with symbolic links. Use pure path conversions for cheap path conversions that do not take the filesystem into account.