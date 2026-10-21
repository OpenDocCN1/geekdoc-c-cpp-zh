`file_size(p)` returns the size of file p in bytes if the file exists as a regular file (on POSIX system, the value is the same as the member `st_size` of the value returned by `stat()`). For all other files, the result is implementation-defined and not portable.

`hard_link_count(p)` returns the number of times a file exists in a file system. Usually, this number is 1, but on some file systems the same file can exist at different locations in the file system (i.e., has different paths). This is different from a symbolic link where a file refers to another file. Here we have a file with a different path for accessing it directly. The file itself is only removed when the last hard link is removed.

# Dealing with the Last Modification

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