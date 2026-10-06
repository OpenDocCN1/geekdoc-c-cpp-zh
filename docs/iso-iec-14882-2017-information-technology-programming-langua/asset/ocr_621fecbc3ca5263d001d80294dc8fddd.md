# ISO/IEC 14882:2017(E)

operating system dependent. [Note: Pathnames "-” and "../" are relative paths. — end note]
18 A symbolic link is a type of file with the property that the file is encountered during pathname resolution, a string stored by the file is used to identify the pathname resolution. [Note: Symbolic links are often called symlinks. A symbolic link can be thought of as a pointer to a file. If the file does not exist, the symbolic link is said to be a "dangling" symbolic link. — end note]

# 30.10.5 Requirements [fs.req]

+   1 Through this subclass, char, wchar_t, char16_t, and char32_t are collectively encoded character types.
2 Functions with template parameters named ECharT shall not participate in overload resolution ECharT is one of the encoded character types.
3 Template parameters named InputIterator shall meet the input requirements (27.2.3) and shall have a value that is one of the encoded character types.
[Note: Use of an encoded character type implies an associated character set and encoding. Since signed and unsigned char have no character set and encoding, they are not permitted types. — end note]

4 Template parameters named Allocator shall meet the Allocator requirements (20.5.3.5).

# 30.10.5.1 Namespaces and headers [fs.req.namespace]

+   1 Unless otherwise, references to entities described in this subclass are assumed to be qualified with ::std::filesystem:

# 30.10.6 Header <filesystem> synopsis [fs.filesystem.syn]

```
namespace filesystem {
// 30.10.8, paths
class path;

// 30.10.8.6, path non-member functions
void swap(path& lhs, path& rhs) noexcept;
size_t hash_value(const path& p) noexcept;

bool operator!=(const path& lhs, const path& rhs) noexcept;
bool operator==(const path lhs, const path rhs) noexcept;
bool operator<(const path lhs, const path rhs) noexcept;
bool operator>(const path lhs, const path rhs) noexcept;
bool operator<=(const path& lhs, const path& rhs) noexcept;
bool operator>=(const path lhs, const path rhs) noexcept;

path operator/(const path lhs, const path rhs);

// 30.10.8.1, path inserter and extractor
template<class charT, class traits>
basic_ostream<charT, traits>
operator<<=(basic_ostream<charT, traits>& os, const path& p);
template<class charT, class traits>
operator>>(basic_istream<charT, traits>& is, const path& p);

// 30.10.8.6.2, path factory functions
template<class Source>
path u8path(const Source& source);
```

©ISO/IEC 2017 - All rights reserved

1238

30.10.6