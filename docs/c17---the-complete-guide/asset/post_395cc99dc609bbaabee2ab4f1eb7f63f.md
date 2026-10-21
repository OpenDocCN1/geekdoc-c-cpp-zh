
If we cannot create the symbolic link because, for example, it already exists or we need special rights, you get something like the following message:

```
EXCEPTION: create_directory_symlink: Can’t create a file when it already exists: "tmp\test\data.txt", "testdir"
path1: "tmp\test\data.txt"
```

or:

```
EXCEPTION: create_directory_symlink: A required privilege is not held by the client.: "test", "tmp\slink"
path1: "test"
```

In any case, note that the situation in a multi-user/multi-process operating system can change at any time, which means that your created directory might even be removed, renamed, or replaced by a regular file after you create it. Therefore, it is simply not possible to ensure the validity of a future request by finding out the current situation. For this reason, is the best approach it usually to try to do what you want (i.e., create a directory, open a file) and process exceptions and errors or validate the expected behavior/outcome.

However, sometimes the attempt to do something with the filesystem might work but not the way you had in mind. For example, if you want to create a file in a specific directory and a symbolic link to another directory already exists, the file is created or overwritten at an unexpected location. This might be OK (the user might have a good reason to create a symbolic link where a directory was expected), but if you want to detect that situation, you have to check for the existence of a file (which is a bit more complicated than you might think at first) before you create something.

Once again: there is no guarantee that results of filesystem checks are still valid when you process them.

## 20.1.4 Dealing with Filesystems Using Parallel Algorithms

See dirsize.cpp for another example using parallel algorithms to accumulate the size of all regular files in a directory tree.

## 20.2 Principles and Terminology

Before discussing the details of the filesystem library, we have to introduce a couple of design principles and some terminology. This is necessary because the standard covers different operating systems and maps them to a common API.

### 20.2.1 General Portability Disclaimer

The C++ Standard does not merely standardize what all possible operating systems have in common for their file systems; in many cases, the C++ Standard follows POSIX standards and requests that implementations follow POSIX as closely as possible. As long as it is reasonable, the behavior should still be there, but with some limitations. If no reasonable behavior is possible, an implementation shall report an error. Possible examples of such errors are:

- Particular characters are not valid to be used as file names
- File system elements that are not supported are created (e.g., symbolic links)
- The differences between specific file systems may still be relevant:
  - Case sensitivity:
    "hello.txt" and "Hello.txt" and "hello.TXT" might refer to the same (Windows) or three different files (POSIX-based).
  - Absolute versus relative paths:
    On some systems, "/bin" is an absolute path (POSIX-based), while on others it is not (Windows).

### 20.2.2 Namespace

The filesystem library has its own sub-namespace filesystem inside std. It is a pretty common convention to introduce the shortcut fs for it:

```
namespace fs = std::filesystem;
```

This allows us to use fs::current_path() instead of std::filesystem::current_path().
Further code examples in this chapter will often use fs as the corresponding shortcut.
Note that you should always qualify the namespace of filesystem calls explicitly, although using argument dependent lookup (ADL) usually works. Not qualifying filesystem calls might sometimes result in unintended behavior.

### 20.2.3 Paths

The key element of the filesystem library is a path. It is a name that represents the (potential) location of a file within a filesystem. It consists of an optional root name, an optional root directory, and a sequence of file names separated by directory separators. The path can be relative (so that the file location depends on the current working directory) or absolute.

Different formats are possible:

- A generic format, which is portable
- A native format, which is specific to the underlying file system

On POSIX-based operating systems there is no difference between the generic and the native format. On Windows, the generic format /tmp/test.txt is a valid native format in addition to \tmp\test.txt, which is also supported (thus, /tmp/test.txt and \tmp\test.txt are two native versions of the same path). On OpenVMS, the corresponding native format might be [tmp]test.txt.

Special file names exist:

- "." represents the current directory
- ".." represents the parent directory

| Path | POSIX normalized | Windows normalized |
|---|---|---|
| foo/.///bar/../ | foo/ | foo\ |
| //host/../foo.txt | //host/foo.txt | \\host\foo.txt |
| ./f/../.f/ | .f/ | .f\ |
| C:/bar/../ | . | C: |
| C:/bar/.. | C:/ | C:\ |
| C:\bar\.. | C:\bar\.. | C:\ |
| /./../data.txt | /data.txt | \data.txt |
| ././ | . | . |

Table 20.1. Effect of Path Normalization

The filesystem library provides functions for both lexical normalization (not taking the filesystem into account) and filesystem-dependent normalization.

### 20.2.5 Member Function versus Free-Standing Functions

The filesystem library provides several functions, which can be both member and free-standing functions. The general approach is:

- **Member functions are cheap.** This is because they are pure lexical operations that do not take the actual filesystem into account, meaning that no operating systems calls are necessary.
  For example:

```
mypath.is_absolute()        // check whether path is absolute or relative
```

- **Free-standing functions are expensive** because they usually take the actual filesystem into account, meaning that operating systems calls are necessary.
  For example:

```
equivalent(path1, path2);    // true if both paths refer to the same file
```

Sometimes, the filesystem library even provides the same functionality operating both lexically and by taking the actual filesystem into account:

```
std::filesystem::path fromP, toP;
...
toP.lexically_relative(fromP);    // yield lexical path from fromP to toP
relative(toP, fromP);             // yield actual path from fromP to toP
```

Due to argument dependent lookup (ADL), in many situations you do not have to specify the full namespace std::filesystem when calling free-standing filesystem functions and an argument has a filesystem-specific type. You only have to qualify the call when implicit conversions from other types are used. For example:

```
create_directory(std::filesystem::path{"tmpdir"});    // OK
remove(std::filesystem::path{"tmpdir"});               // OK
std::filesystem::create_directory("tmpdir");           // OK
std::filesystem::remove("tmpdir");                     // OK
```

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

### 20.2.6 Error Handling

As discussed with the second example, filesystems are a source of errors. You have to take into account that necessary files might not exist, file operations might not be allowed, or operations might violate resource limits. In addition, while a program is running other processes might create, modify, or remove files meaning that advance checks are no guarantee for no errors.

The problem is that in principle, you cannot ensure ahead of time that the next filesystem operation will succeed. Any result of a check might no longer be valid when you process it. Therefore, the best approach is usually to perform one or more filesystem operations and deal with resulting exceptions or errors.

Note also that when reading/writing with regular files, by default, the I/O streams library does not throw on errors. It converts any operation into a no-op instead. Therefore, the recommendation is to at least check whether files could successfully be opened.

Because dealing with exceptions is not always appropriate (such as when you want to react directly to a failed filesystem call), the filesystem library uses a mixed approach when dealing with the filesystem:

- By default, filesystem errors are handled as exceptions.
- However, you can handle specific errors locally if you have or want to.

Therefore, filesystem operations usually have two overloads for each operation:

1. By default (without an additional error handling argument), the operations throw a filesystem_error exceptions on errors.
2. By passing an additional out parameter, you can get an error code on error instead.

Note that in the latter case, you might still have special return values, signaling a specific error that is not handled as an exception.

### Using filesystem_error Exceptions

For example, you can try to create a directory as follows:

```
if (!create_directory(p)) {
    std::cout << p << " already exists\n";    // path exists
}    // exception on error (unless path exists)
```
