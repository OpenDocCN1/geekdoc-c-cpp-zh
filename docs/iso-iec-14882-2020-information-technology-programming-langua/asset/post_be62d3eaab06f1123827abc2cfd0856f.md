
# ISO/IEC 14882:2020(E)

## 28.4.8.3 Class template messages_byname [locale.messages.byname]

```
namespace std {
    template<class charT>
        class messages_byname : public messages<charT> {
        public:
            using catalog    = messages_base::catalog;
            using string_type = basic_string<charT>;

            explicit messages_byname(const char*, size_t refs = 0);
            explicit messages_byname(const string&, size_t refs = 0);

        protected:
            ~messages_byname();
        };
    }
```

## 28.5 C library locales [c.locales]

## 28.5.1 Header <clocale> synopsis [clocale.syn]

```
namespace std {
    struct lconv;

    char* setlocale(int category, const char* locale);
    lconv* localeconv();
}
```

#define NULL see 17.2.3
#define LC_ALL see below
#define LC_COLLATE see below
#define LC_CTYPE see below
#define LC_MONETARY see below
#define LC_NUMERIC see below
#define LC_TIME see below

1 The contents and meaning of the header <clocale> are the same as the C standard library header <locale.h>.

## 28.5.2 Data races [clocale.data.races]

1 Calls to the function setlocale may introduce a data race (16.4.6.10) with other calls to setlocale or with calls to the functions listed in Table 114.

See also: ISO C 7.11

Table 114: Potential setlocale data races [tab:setlocale.data.races]

| fprintf | isprint | iswdigit | localeconv | tolower |
| fscanf | ispunct | iswgraph | mblen | toupper |
| isalnum | isspace | iswlower | mbstowcs | towlower |
| isalpha | isupper | iswprint | mbtowc | towupper |
| isblank | iswalnum | iswpunct | setlocale | wcscoll |
| iscntrl | iswalpha | iswspace | strcoll | wcstod |
| isdigit | iswblank | iswupper | strerror | wcstombs |
| isgraph | iswcntrl | iswxdigit | strtod | wcsxfrm |
| islower | iswctype | isxdigit | strxfrm | wctomb |
| islower | iswctype | isxdigit | strxfrm | wctomb |

## 29.2.2 Positioning type limitations [iostream.limits.pos]

1 The classes of Clause 29 with template arguments charT and traits behave as described if traits::pos_type and traits::off_type are streampos and streamoff respectively. Except as noted explicitly below, their behavior when traits::pos_type and traits::off_type are other types is implementation-defined.

2 In the classes of Clause 29, a template parameter with name charT represents a member of the set of types containing char, wchar_t, and any other implementation-defined character types that meet the requirements for a character on which any of the iostream components can be instantiated.

## 29.2.3 Thread safety [iostream.threadsafety]

1 Concurrent access to a stream object (29.8, 29.9), stream buffer object (29.6), or C Library stream (29.12) by multiple threads may result in a data race (6.9.2) unless otherwise specified (29.4).

> [Note 1: Data races result in undefined behavior (6.9.2). — end note]

2 If one thread makes a library call a that writes a value to a stream and, as a result, another thread reads this value from the stream through a library call b such that this does not result in a data race, then a's write synchronizes with b's read.

## 29.3 Forward declarations [iostream.forward]

## 29.3.1 Header <iosfwd> synopsis [iosfwd.syn]

```
namespace std {
  template<class charT> struct char_traits;
  template<> struct char_traits<char>;
  template<> struct char_traits<char8_t>;
  template<> struct char_traits<char16_t>;
  template<> struct char_traits<char32_t>;
  template<> struct char_traits<wchar_t>;

  template<class T> class allocator;

  template<class charT, class traits = char_traits<charT>>
    class basic_ios;
  template<class charT, class traits = char_traits<charT>>
    class basic_streambuf;
  template<class charT, class traits = char_traits<charT>>
    class basic_istream;
  template<class charT, class traits = char_traits<charT>>
    class basic_ostream;
  template<class charT, class traits = char_traits<charT>>
    class basic_iostream;

  template<class charT, class traits = char_traits<charT>,
           class Allocator = allocator<charT>>
    class basic_stringbuf;
  template<class charT, class traits = char_traits<charT>,
           class Allocator = allocator<charT>>
    class basic_istringstream;
  template<class charT, class traits = char_traits<charT>,
           class Allocator = allocator<charT>>
    class basic_ostringstream;
  template<class charT, class traits = char_traits<charT>,
           class Allocator = allocator<charT>>
    class basic_stringstream;

  template<class charT, class traits = char_traits<charT>>
    class basic_filebuf;
  template<class charT, class traits = char_traits<charT>>
    class basic_ifstream;
  template<class charT, class traits = char_traits<charT>>
    class basic_ofstream;
  template<class charT, class traits = char_traits<charT>>
    class basic_fstream;
}
```

# ISO/IEC 14882:2020(E)

(3.1) — static int index, specifies the next available unique index for the integer or pointer arrays maintained for the private use of the program, initialized to an unspecified value;

(3.2) — long* iarray, points to the first element of an arbitrary-length long array maintained for the private use of the program;

(3.3) — void** parray, points to the first element of an arbitrary-length pointer array maintained for the private use of the program.

— end note]

## 29.5.3.2 Types [ios.types]

## 29.5.3.2.1 Class ios_base::failure [ios.failure]

```
namespace std {
class ios_base::failure : public system_error {
public:
    explicit failure(const string& msg, const error_code& ec = io_errc::stream);
    explicit failure(const char* msg, const error_code& ec = io_errc::stream);
};
}
```

1 An implementation is permitted to define ios_base::failure as a synonym for a class with equivalent functionality to class ios_base::failure shown in this subclause.

> [Note 1: When ios_base::failure is a synonym for another type, that type is required to provide a nested type failure to emulate the injected-class-name. — end note]

The class failure defines the base class for the types of all objects thrown as exceptions, by functions in the iostreams library, to report errors detected during stream buffer operations.

2 When throwing ios_base::failure exceptions, implementations should provide values of ec that identify the specific reason for the failure.

> [Note 2: Errors arising from the operating system would typically be reported as system_category() errors with an error value of the error number reported by the operating system. Errors arising from within the stream library would typically be reported as error_code(io_errc::stream, iostream_category()). — end note]

```
explicit failure(const string& msg, const error_code& ec = io_errc::stream);
```

3 Effects: Constructs the base class with msg and ec.

```
explicit failure(const char* msg, const error_code& ec = io_errc::stream);
```

4 Effects: Constructs the base class with msg and ec.

## 29.5.3.2.2 Type ios_base::fmtflags [ios.fmtflags]

```
using fmtflags = T1;
```

1 The type fmtflags is a bitmask type (16.3.3.3.4). Setting its elements has the effects indicated in Table 116.

2 Type fmtflags also defines the constants indicated in Table 117.

## 29.5.3.2.3 Type ios_base::iostate [ios.iostate]

```
using iostate = T2;
```

1 The type iostate is a bitmask type (16.3.3.3.4) that contains the elements indicated in Table 118.

2 Type iostate also defines the constant:

+   (2.1) — goodbit, the value zero.

## 29.5.3.2.4 Type ios_base::openmode [ios.openmode]

```
using openmode = T3;
```

1 The type openmode is a bitmask type (16.3.3.3.4). It contains the elements indicated in Table 119.

## 29.5.3.2.5 Type ios_base::seekdir [ios.seekdir]

```
using seekdir = T4;
```

1 The type seekdir is an enumerated type (16.3.3.3.3) that contains the elements indicated in Table 120.
