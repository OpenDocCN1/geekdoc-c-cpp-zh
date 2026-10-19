# ISO/IEC 14882:2020(E)

to the `filesystem_error` constructor with a single path argument. For functions with two path arguments, the first of these arguments shall be passed to the `filesystem_error` constructor as the `path1` argument, and the second shall be passed as the `path2` argument. The `filesystem_error` constructor’s `error_code` argument is set as appropriate for the specific operating system dependent error.

+   (2.2) — Failure to allocate storage is reported by throwing an exception as described in 16.4.6.13.

+   (2.3) — Destructors throw nothing.

3 Functions having an argument of type `error_code&` handle errors as follows, unless otherwise specified:

+   (3.1) — If a call by the implementation to an operating system or other underlying API results in an error that prevents the function from meeting its specifications, the `error_code&` argument is set as appropriate for the specific operating system dependent error. Otherwise, `clear()` is called on the `error_code&` argument.

# 29.11.6 Class path [fs.class.path]

# 29.11.6.1 General [fs.class.path.general]

1 An object of class `path` represents a path and contains a pathname. Such an object is concerned only with the lexical and syntactic aspects of a path. The path does not necessarily exist in external storage, and the pathname is not necessarily valid for the current operating system or for a particular file system.

> [Note 1: Class `path` is used to support the differences between the string types used by different operating systems to represent pathnames, and to perform conversions between encodings when necessary. — end note]

3 A *path* is a sequence of elements that identify the location of a file within a filesystem. The elements are the *root-name*opt, *root-directory*opt, and an optional sequence of *filenames* (29.11.6.2). The maximum number of elements in the sequence is operating system dependent (29.11.2.3).

4 An *absolute path* is a path that unambiguously identifies the location of a file without reference to an additional starting location. The elements of a path that determine if it is absolute are operating system dependent. A *relative path* is a path that is not absolute, and as such, only unambiguously identifies the location of a file when resolved relative to an implied starting location. The elements of a path that determine if it is relative are operating system dependent.

> [Note 2: Pathnames “.” and “..” are relative paths. — end note]

5 A *pathname* is a character string that represents the name of a path. Pathnames are formatted according to the generic pathname format grammar (29.11.6.2) or according to an operating system dependent *native pathname format* accepted by the host operating system.

6 *Pathname resolution* is the operating system dependent mechanism for resolving a pathname to a particular file in a file hierarchy. There may be multiple pathnames that resolve to the same file.

> [Example 1: POSIX specifies the mechanism in section 4.11, Pathname resolution. — end example]

```
namespace std::filesystem {
  class path {
  public:
    using value_type  = see below;
    using string_type = basic_string<value_type>;
    static constexpr value_type preferred_separator = see below;

    // 29.11.8.1, enumeration format
    enum format;

    // 29.11.6.5.1, constructors and destructor
    path() noexcept;
    path(const path& p);
    path(path&& p) noexcept;
    path(string_type&& source, format fmt = auto_format);
    template<class Source>
      path(const Source& source, format fmt = auto_format);
    template<class InputIterator>
      path(InputIterator first, InputIterator last, format fmt = auto_format);
    template<class Source>
      path(const Source& source, const locale& loc, format fmt = auto_format);
```