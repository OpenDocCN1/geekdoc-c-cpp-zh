
replace_extension() replaces, adds, or removes an extension:

- If the file has an extension, it is replaced.
- If the file has no extension, the new extension is added.
- If you skip the new extension or the new extension is empty, any existing extension is removed.

It does not matter whether you place a leading dot in the replacement. The function ensures that there is exactly one dot between the stem and the extension of the resulting file name. For example:

```
fs::path("file.txt").replace_extension("tmp")      // file.tmp
fs::path("file.txt").replace_extension(".tmp")     // file.tmp
fs::path("file.txt").replace_extension("")         // file
fs::path("file.txt").replace_extension()            // file
fs::path("dir").replace_extension("tmp")           // dir.tmp
fs::path(".git").replace_extension("tmp")          // .git.tmp
```

Note that file names that are “pure extensions” (such as .git) do not count as extensions.

## 20.3.6 Path Comparisons

Table Path Comparisons lists the operations you can use to compare two different paths.

| Call | Effect |
|---|---|
| p1 == p2 | Yields whether two paths are equal |
| p1 != p2 | Yields whether two paths are not equal |
| p1 < p2 | Yields whether a path is less than another |
| p1 <= p2 | Yields whether a path is less than or equal to another |
| p1 >= p2 | Yields whether a path is greater than or equal to another |
| p1 > p2 | Yields whether a path is greater than another |
| p.compare(p2) | Yields whether p2 is less than, equal to, or greater than p |
| p.compare(sv) | Yields whether p2 is less than, equal to, or greater than the string (view) sv converted to a path |
| equivalent(p1, p2) | Expensive path comparison taking the filesystem into account |

Table 20.8. Path Comparisons

Note that most of the comparisons do not take the filesystem into account, which means that they operate only lexically, which is cheap but may result in surprising return values:

- Using ==, != and compare() the following paths are all different:

```
tmp1/f
./tmp1/f
tmp1/./f
tmp1/tmp11/../f
```

## 20.3 Path Operations

• Only different formats for specifying a directory separator are detected. Thus, the following paths are all equal (provided the backslash is a valid directory separator):

```
tmp1/f
/tmp1/f
tmp1\f
tmp1\/f
```

It is only if you call lexically_normal() for each path that all of the paths above are equal (provided the backslash is a valid directory separator). For example:

```
std::filesystem::path p1{"tmp1/f"};
std::filesystem::path p2{"../tmp1/f"};
```

```
p1 == p2 //true
p1.compare(p2) //not 0
p1.lexically_normal() == p2.lexically_normal() //true
p1.lexically_normal().compare(p2.lexically_normal()) //0
```

If you want to take the filesystem into account so that symbolic links are handled correctly, you can use equivalent(). However, note that this function requires that both paths represent existing files. Thus, a generic way to compare paths as accurately as possible (which does not have the best performance) is as follows:

```
bool pathsAreEqual(const std::filesystem::path& p1, const std::filesystem::path& p2)
{
	return exists(p1) && exists(p2) ? equivalent(p1, p2)
		: p1.lexically_normal() == p2.lexically_normal();
}
```

## 20.3.7 Other Path Operations

Table Other Path Operations lists the remaining path operations not listed yet.

| Call | Effect |
|------|--------|
| p.hash_value() | Yields the hash value for a path |

Note that only equal paths are guaranteed to have the same hash value. The following paths yield different hash values:

- tmp1/f
- ./tmp1/f
- /tmp1/./f
- tmp1/tmp11/../f

Therefore, you might want to normalize paths before you put them in a hash table.

## Check for Existence of a File

exists() answers the question of whether there is effectively a file to open. Thus, as just discussed, it follows symbolic links. Therefore, it yields false if there is a symbolic link to a non-existing file.

As a consequence, code like this does not work as expected:

```
// if not done yet, create a symbolic link to file:
if (!exists(p)) {            // OOPS: checks if the file p refers to doesn't exist
    std::filesystem::create_symlink(file, p);
}
```

If p already exists as a symbolic link to a non-existing file, create_symlink() will try to create the symbolic link at the location where the symbolic link already exists and raise a corresponding exception.

Because the situation in a multi-user/multi-process filesystem can change at any time, the best approach is usually to try to perform an operation and handle the error if it fails. Thus, we can simply call the operation and handle a corresponding exception or handle an error code passed as an additional argument.

However, sometimes you need to check for the existence of a file (before performing a filesystem operation). For example, if you want to create a file at a specific location and there is already a symbolic link, the file is created or is overwritten at a (possibly) unexpected location. In that case, you should check for the existence of a file as follows:

```
if (!exists(symlink_status(p))) {  // OK: checks if p doesn't exist yet (as symbolic link)
    ...
}
```

Here, we use symlink_status(), which yields the status that does not follow symbolic links, to check for the existence of any file at the location of p.

## Other File Attributes

Table Operations for File Attributes lists a couple of free-standing functions for checking for additional file attributes.

| Call | Effect |
|---|---|
| is_empty(p) | Yields whether the file is empty |
| file_size(p) | Yields the size of a file |
| hard_link_count(p) | Yields the number of hard links |
| last_write_time(p) | Yields the timepoint of the last write to a file |

Table 20.11. Operations for File Attributes

Note that there is a difference between whether a path is empty and whether the file specified by a path is empty:

```
p.empty()     // true if path p is empty (cheap operation)
is_empty(p)   // true if file at path p is empty (filesystem operation)
```

6 Thanks to Billy O'Neal for pointing this out.

`file_size(p)` returns the size of file p in bytes if the file exists as a regular file (on POSIX system, the value is the same as the member `st_size` of the value returned by `stat()`). For all other files, the result is implementation-defined and not portable.

`hard_link_count(p)` returns the number of times a file exists in a file system. Usually, this number is 1, but on some file systems the same file can exist at different locations in the file system (i.e., has different paths). This is different from a symbolic link where a file refers to another file. Here we have a file with a different path for accessing it directly. The file itself is only removed when the last hard link is removed.

## Dealing with the Last Modification

`last_write_time(p)` returns the timepoint of the last modification or write access of the file. The return type is a special time_point type of the standard chrono library for timepoints:

```
namespace std::filesystem {
    using file_time_type = chrono::time_point<trivialClock>;
}
```

The clock type `trivialClock` is an implementation-specific clock type that reflects the resolution and range of filesystem time values. For example, you can use it as follows:

```
void printFileTime(const std::filesystem::path& p)
{
    auto filetime = last_write_time(p);
    auto diff = std::filesystem::file_time_type::clock::now() - filetime;
    std::cout << p << " is "
              << std::chrono::duration_cast<std::chrono::seconds>(diff).count()
              << " Seconds old.\n";
}
```

which might output:

```
"fileattr.cpp" is 4 Seconds old.
```

Instead of

```
std::filesystem::file_time_type::clock::now()
```

in this example, you could also write:

```
decltype(filetime)::clock::now()
```

Note that the clock used by a filesystem timepoint is not guaranteed to be the standard system_clock. Therefore, there is currently no standardized support for converting the filesystem timepoint into type time_t to use it as absolute time in strings or output.⁷ There is a workaround though. The following function "roughly" converts a timepoint of any clock into a time_t object:

```
template<typename TimePoint>
std::time_t toTimeT(TimePoint tp)
{
```
