Using `operator/` to concatenate paths is clever and looks good. With `p /=...`, you could directly append an element to `p`. Both correspond to append.
When you use `concat`, `+`, or `+=`, you extend the last path component, adding without `/`.

> **Windows, Unix, and Embedded**
> 
> On some extremely lightweight platforms, `<filesystem>` will not be available to you. However, the authors of this part of the standard library have managed to unify both the Windows and Unix worlds.
> 
> This part of the library is also somewhat heavier and likely not implemented as “header-only.” I read a note that the `-lstdc++fs` option when linking with GCC and `-lc++fs` with Clang must be specified. However, this was no longer the case for me.

To give you an idea of the capabilities of filesystem, I will provide an excerpt from the long list of features:

+   - **copy_file, rename, remove, remove_all**  
+     Simple copying or renaming of a file as well as removing a single file or recursively all files in a directory.
+   - **current_path**  
+     Returns the current directory.
+   - **exists, equivalent**  
+     `exists` checks if a file exists; `equivalent` checks if two different path instances refer to the same file.
+   - **file_size, is_empty, is_regular_file**  
+     Provide various information about a file.

# 27.10  Formatting

Since C++20, there is a new way to format data. In the `<format>` header, the following elements are the most important:

+   - **format**  
+     Formats any number of arguments into a string according to a provided format.
+   - **format_to**  
+     Formats into a buffer or iterator.
+   - **format_to_n**  
+     Formats into a buffer up to a specified length.
+   - **format_size**  
+     Determines the length of a formatted output so you can allocate enough space for a buffer.