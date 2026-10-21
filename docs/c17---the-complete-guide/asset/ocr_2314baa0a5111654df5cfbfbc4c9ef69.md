+   - File system elements that are not supported are created (e.g., symbolic links)
+   The differences between specific file systems may still be relevant:
+   - Case sensitivity:
+     "hello.txt" and "Hello.txt" and "hello.TXT" might refer to the same (Windows) or three different files (POSIX-based).
+   - Absolute versus relative paths:
+     On some systems, "/bin" is an absolute path (POSIX-based), while on others it is not (Windows).

# 20.2.2 Namespace

The filesystem library has its own sub-namespace filesystem inside std. It is a pretty common convention to introduce the shortcut fs for it:

```
namespace fs = std::filesystem;
```

This allows us to use fs::current_path() instead of std::filesystem::current_path().
Further code examples in this chapter will often use fs as the corresponding shortcut.
Note that you should always qualify the namespace of filesystem calls explicitly, although using argument dependent lookup (ADL) usually works. Not qualifying filesystem calls might sometimes result in unintended behavior.

# 20.2.3 Paths

The key element of the filesystem library is a path. It is a name that represents the (potential) location of a file within a filesystem. It consists of an optional root name, an optional root directory, and a sequence of file names separated by directory separators. The path can be relative (so that the file location depends on the current working directory) or absolute.

Different formats are possible:

+   - A generic format, which is portable
+   - A native format, which is specific to the underlying file system

On POSIX-based operating systems there is no difference between the generic and the native format. On Windows, the generic format /tmp/test.txt is a valid native format in addition to \tmp\test.txt, which is also supported (thus, /tmp/test.txt and \tmp\test.txt are two native versions of the same path). On OpenVMS, the corresponding native format might be [tmp]test.txt.

Special file names exist:

+   - "." represents the current directory
+   - ".." represents the parent directory