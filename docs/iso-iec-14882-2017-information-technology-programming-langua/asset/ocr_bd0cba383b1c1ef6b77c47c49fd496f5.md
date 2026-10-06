# ISO/IEC 14882:2017(E)

```
template <class EChar, class traits = char_traits<EChar>,
class Allocator = allocator<EChar>>
basic_string<EChar, traits, Allocator>
    string(const Allocator& a = Allocator()) const;
```

6 Returns: native().

7 Remarks: All memory allocation, including for the return value, shall be performed by a. Conversion,
if any, is specified by 30.10.8.2.

```
std::string string() const;
std::wstring wstring() const;
std::ustring ustring() const;
std::u16string u16string() const;
std::u32string u32string() const;
```

8 Returns: pathname.

9 Remarks: Conversion, if any, is performed as specified by 30.10.8.2. The encoding of the string
is always UTF-8.

# 30.10.8.4.7 path generic format observers [fs.path.generic]

+   1 Generic object function returns strings formatted to the generic pathname format
(30.10.8.1). A single slash ('/') character is used as the directory-separator.

+   2 Example: On an operating system uses backslashes as its preferred-separator,
path("home\bar").generic_string()
returns "home/bar".-- end example

```
template <class EChar, class traits = char_traits<EChar>,
class Allocator = allocator<EChar>>
basic_string<EChar, traits, Allocator>
generic_string(const Allocator& a = Allocator()) const;
```

3 Returns: The pathname in the generic format.

4 Remarks: All memory allocation, including for the return value, shall be performed by a. Conversion,
if any, is specified by 30.10.8.2.

```
std::string generic_string() const;
std::wstring generic_wstring() const;
std::ustring generic_ustring() const;
std::u16string generic_u16string() const;
std::u32string generic_u32string() const;
```

5 Returns: The pathname in the generic format.

6 Remarks: Conversion, if any, is specified by 30.10.8.2. The encoding of the string returned by generic_ustring() is always UTF-8.

# 30.10.8.4.8 path compare [fs.path.compare]

```
int compare(const path& p) const noexcept;
```

1 Returns:

+   - a value less than 0, if native() for the elements of *this are lexicographically less than native()
for the elements of p; otherwise,

+   - a value greater than 0, if native() for the elements of *this are lexicographically greater than
native() for the elements of p; otherwise,

§ 30.10.8.4.8 ©ISO/IEC 2017 - All rights reserved 1253