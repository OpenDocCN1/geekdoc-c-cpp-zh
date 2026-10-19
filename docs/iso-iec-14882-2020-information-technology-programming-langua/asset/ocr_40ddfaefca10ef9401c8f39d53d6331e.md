# ISO/IEC 14882:2020(E)

(2.2) — the qualified-id iterator_traits<decay_t<Source>>::value_type is valid and denotes a possibly const encoded character type (13.10.3).

> 3 [Note 1: See path conversions (29.11.6.3) for how the value types above and their encodings convert to path::value_type and its encoding. — end note]

4 Arguments of type Source shall not be null pointers.

# 29.11.6.5 Members [fs.path.member]

# 29.11.6.5.1 Constructors [fs.path.construct]

```
path() noexcept;
```

1 Postconditions: empty() == true.

```
path(const path& p);
path(path&& p) noexcept;
```

2 Effects: Constructs an object of class path having the same pathname in the native and generic formats, respectively, as the original value of p. In the second form, p is left in a valid but unspecified state.

```
path(string_type&& source, format fmt = auto_format);
```

3 Effects: Constructs an object of class path for which the pathname in the detected-format of source has the original value of source (29.11.6.3.1), converting format if required (29.11.6.3.1). source is left in a valid but unspecified state.

```
template<class Source>
  path(const Source& source, format fmt = auto_format);
template<class InputIterator>
  path(InputIterator first, InputIterator last, format fmt = auto_format);
```

4 Effects: Let s be the effective range of source (29.11.6.4) or the range [first, last), with the encoding converted if required (29.11.6.3). Finds the detected-format of s (29.11.6.3.1) and constructs an object of class path for which the pathname in that format is s.

```
template<class Source>
  path(const Source& source, const locale& loc, format fmt = auto_format);
template<class InputIterator>
  path(InputIterator first, InputIterator last, const locale& loc, format fmt = auto_format);
```

5 Mandates: The value type of Source and InputIterator is char.

6 Effects: Let s be the effective range of source or the range [first, last), after converting the encoding as follows:

+   (6.1) — If value_type is wchar_t, converts to the native wide encoding (29.11.6.3.2) using the codecvt<wchar_t, char, mbstate_t> facet of loc.
+   (6.2) — Otherwise a conversion is performed using the codecvt<wchar_t, char, mbstate_t> facet of loc, and then a second conversion to the current ordinary encoding.

7 Finds the detected-format of s (29.11.6.3.1) and constructs an object of class path for which the pathname in that format is s.

> [Example 1: A string is to be read from a database that is encoded in ISO/IEC 8859-1, and used to create a directory:

```
namespace fs = std::filesystem;
std::string latin1_string = read_latin1_data();
codecvt_8859_1<wchar_t> latin1_facet;
std::locale latin1_locale(std::locale(), latin1_facet);
fs::create_directory(fs::path(latin1_string, latin1_locale));
```

For POSIX-based operating systems, the path is constructed by first using latin1_facet to convert ISO/IEC 8859-1 encoded latin1_string to a wide character string in the native wide encoding (29.11.6.3.2). The resulting wide string is then converted to an ordinary character pathname string in the current native ordinary encoding. If the native wide encoding is UTF-16 or UTF-32, and the current native ordinary encoding is UTF-8, all of the characters in the ISO/IEC 8859-1 character set will be converted to their Unicode representation, but for other native ordinary encodings some characters may have no representation.