```
create_directory("tmpdir");        // ERROR
```

The last call will fail to compile because we do not pass an argument of the filesystem namespace meaning that the symbol create_directory is not looked up in that namespace.

However, there is a famous trap:

```
remove("tmpdir");      // OOPS: calls C function remove()
```

Depending on the header file you include (indirectly), this call might compile finding the C function remove(), which behaves slightly differently: it might also remove the specified file but might not remove empty directories.

Therefore, the strong recommendation is to explicitly qualify all free-standing filesystem calls. For example:

```
namespace fs = std::filesystem;
...
fs::remove("tmpdir");  // OK: calls C++ filesystem function remove()
```

# 20.2.6 Error Handling

As discussed with the second example, filesystems are a source of errors. You have to take into account that necessary files might not exist, file operations might not be allowed, or operations might violate resource limits. In addition, while a program is running other processes might create, modify, or remove files meaning that advance checks are no guarantee for no errors.

The problem is that in principle, you cannot ensure ahead of time that the next filesystem operation will succeed. Any result of a check might no longer be valid when you process it. Therefore, the best approach is usually to perform one or more filesystem operations and deal with resulting exceptions or errors.

Note also that when reading/writing with regular files, by default, the I/O streams library does not throw on errors. It converts any operation into a no-op instead. Therefore, the recommendation is to at least check whether files could successfully be opened.

Because dealing with exceptions is not always appropriate (such as when you want to react directly to a failed filesystem call), the filesystem library uses a mixed approach when dealing with the filesystem:

+   - By default, filesystem errors are handled as exceptions.
+   - However, you can handle specific errors locally if you have or want to.

Therefore, filesystem operations usually have two overloads for each operation:

+   1. By default (without an additional error handling argument), the operations throw a filesystem_error exceptions on errors.
+   2. By passing an additional out parameter, you can get an error code on error instead.

Note that in the latter case, you might still have special return values, signaling a specific error that is not handled as an exception.

# Using filesystem_error Exceptions

For example, you can try to create a directory as follows:

```
if (!create_directory(p)) {
    std::cout << p << " already exists\n";    // path exists
}    // exception on error (unless path exists)
```