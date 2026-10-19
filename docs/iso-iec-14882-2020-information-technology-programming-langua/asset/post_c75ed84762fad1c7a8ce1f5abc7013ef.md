
## ISO/IEC 14882:2020(E)

2 [Note 1: The class template basic_filebuf treats a file as a source or sink of bytes. In an environment that uses a large character set, the file typically holds multibyte character sequences and the basic_filebuf object converts those multibyte sequences into wide character sequences. — end note]

3 In subclause 29.9, member functions taking arguments of const filesystem::path::value_type* are only provided on systems where filesystem::path::value_type (29.11.6) is not char.

> [Note 2: These functions enable class path support for systems with a wide native path character type, such as wchar_t. — end note]

## 29.9.2 Class template basic_filebuf [filebuf]

### 29.9.2.1 General [filebuf.general]

```
namespace std {
template<class charT, class traits = char_traits<charT>>
class basic_filebuf : public basic_streambuf<charT, traits> {
public:
    using char_type = charT;
    using int_type = typename traits::int_type;
    using pos_type = typename traits::pos_type;
    using off_type = typename traits::off_type;
    using traits_type = traits;

    // 29.9.2.2, constructors/destructor
    basic_filebuf();
    basic_filebuf(const basic_filebuf&) = delete;
    basic_filebuf(basic_filebuf&& rhs);
    virtual ~basic_filebuf();

    // 29.9.2.3, assign and swap
    basic_filebuf& operator=(const basic_filebuf&) = delete;
    basic_filebuf& operator=(basic_filebuf&& rhs);
    void swap(basic_filebuf& rhs);

    // 29.9.2.4, members
    bool is_open() const;
    basic_filebuf* open(const char* s, ios_base::openmode mode);
    basic_filebuf* open(const filesystem::path::value_type* s, ios_base::openmode mode); // wide systems only; see 29.9.1
    basic_filebuf* open(const string& s, ios_base::openmode mode);
    basic_filebuf* open(const filesystem::path& s, ios_base::openmode mode);
    basic_filebuf* close();

protected:
    // 29.9.2.5, overridden virtual functions
    streamsize showmanyc() override;
    int_type underflow() override;
    int_type uflow() override;
    int_type pbackfail(int_type c = traits::eof()) override;
    int_type overflow (int_type c = traits::eof()) override;

    basic_streambuf<charT, traits>* setbuf(char_type* s, streamsize n) override;
    pos_type seekoff(off_type off, ios_base::seekdir way, ios_base::openmode which = ios_base::in | ios_base::out) override;
    pos_type seekpos(pos_type sp, ios_base::openmode which = ios_base::in | ios_base::out) override;
    int sync() override;
    void imbue(const locale& loc) override;
};

template<class charT, class traits>
    void swap(basic_filebuf<charT, traits>& x,
              basic_filebuf<charT, traits>& y);
}
```

1 The class basic_filebuf<charT, traits> associates both the input sequence and the output sequence with a file.

2 The restrictions on reading and writing a sequence controlled by an object of class basic_filebuf<charT, traits> are the same as for reading and writing with the C standard library FILEs.

3 In particular:

- (3.1) — If the file is not open for reading the input sequence cannot be read.
- (3.2) — If the file is not open for writing the output sequence cannot be written.
- (3.3) — A joint file position is maintained for both the input sequence and the output sequence.

4 An instance of basic_filebuf behaves as described in 29.9.2 provided traits::pos_type is fpos<traits::state_type>. Otherwise the behavior is undefined.

5 In order to support file I/O and multibyte/wide character conversion, conversions are performed using members of a facet, referred to as a_codecvt in following subclauses, obtained as if by

```
const codecvt<charT, char, typename traits::state_type>& a_codecvt =
    use_facet<codecvt<charT, char, typename traits::state_type>>(getloc());
```

### 29.9.2.2 Constructors [filebuf.cons]

```
basic_filebuf();
```

1 Effects: Initializes the base class with basic_streambuf<charT, traits>() (29.6.3.2).

2 Postconditions: is_open() == false.

```
basic_filebuf(basic_filebuf&& rhs);
```

3 Effects: It is implementation-defined whether the sequence pointers in *this (eback(), gptr(), egptr(), pbase(), pptr(), epptr()) obtain the values which rhs had. Whether they do or not, *this and rhs reference separate buffers (if any at all) after the construction. Additionally *this references the file which rhs did before the construction, and rhs references no file after the construction. The openmode, locale and any other state of rhs is also copied.

4 Postconditions: Let rhs_p refer to the state of rhs just prior to this construction and let rhs_a refer to the state of rhs just after this construction.

- (4.1) — is_open() == rhs_p.is_open()
- (4.2) — rhs_a.is_open() == false
- (4.3) — gptr() - eback() == rhs_p.gptr() - rhs_p.eback()
- (4.4) — egptr() - eback() == rhs_p.egptr() - rhs_p.eback()
- (4.5) — pptr() - pbase() == rhs_p.pptr() - rhs_p.pbase()
- (4.6) — epptr() - pbase() == rhs_p.epptr() - rhs_p.pbase()
- (4.7) — if (eback()) eback() != rhs_a.eback()
- (4.8) — if (gptr()) gptr() != rhs_a.gptr()
- (4.9) — if (egptr()) egptr() != rhs_a.egptr()
- (4.10) — if (pbase()) pbase() != rhs_a.pbase()
- (4.11) — if (pptr()) pptr() != rhs_a.pptr()
- (4.12) — if (epptr()) epptr() != rhs_a.epptr()

```
virtual ~basic_filebuf();
```

5 Effects: Calls close(). If an exception occurs during the destruction of the object, including the call to close(), the exception is caught but not rethrown (see 16.4.6.13).

### 29.9.2.3 Assignment and swap [filebuf.assign]

```
basic_filebuf& operator=(basic_filebuf&& rhs);
```

1 Effects: Calls close() then move assigns from rhs. After the move assignment *this has the observable state it would have had if it had been move constructed from rhs (see 29.9.2.2).

2 Returns: *this.

```
void swap(basic_filebuf& rhs);
```

3 Effects: Exchanges the state of *this and rhs.

```
template<class charT, class traits>
    void swap(basic_filebuf<charT, traits>& x,
        basic_filebuf<charT, traits>& y);
```

4 Effects: Equivalent to: x.swap(y).

### 29.9.2.4 Member functions [filebuf.members]

```
bool is_open() const;
```

1 Returns: true if a previous call to open succeeded (returned a non-null value) and there has been no intervening call to close.

```
basic_filebuf* open(const char* s, ios_base::openmode mode);
basic_filebuf* open(const filesystem::path::value_type* s,
    ios_base::openmode mode); // wide systems only; see 29.9.1
```

2 Preconditions: s points to a NTCTS (3.32).

3 Effects: If is_open() != false, returns a null pointer. Otherwise, initializes the filebuf as required. It then opens the file to which s resolves, if possible, as if by a call to fopen with the second argument determined from mode & ~ios_base::ate as indicated in Table 126. If mode is not some combination of flags shown in the table then the open fails.

Table 126: File open modes [tab:filebuf.open.modes]

| binary | in | out | trunc | app | stdio equivalent |
|--------|----|-----|-------|-----|------------------|
|        |    |  +  |       |     | "w"              |
|        |    |  +  |       |  +  | "a"              |
|        |    |     |       |  +  | "a"              |
|        |    |  +  |   +   |     | "w"              |
|        |  + |     |       |     | "r"              |
|        |  + |  +  |       |     | "r+"             |
|        |  + |  +  |   +   |     | "w+"             |
|        |  + |  +  |       |  +  | "a+"             |
|        |  + |     |       |  +  | "a+"             |
|    +   |    |  +  |       |     | "wb"             |
|    +   |    |  +  |       |  +  | "ab"             |
|    +   |    |     |       |  +  | "ab"             |
|    +   |    |  +  |   +   |     | "wb"             |
|    +   |  + |     |       |     | "rb"             |
|    +   |  + |  +  |       |     | "r+b"            |
|    +   |  + |  +  |   +   |     | "w+b"            |
|    +   |  + |  +  |       |  +  | "a+b"            |
|    +   |  + |     |       |  +  | "a+b"            |

4 If the open operation succeeds and ios_base::ate is set in mode, positions the file to the end (as if by calling fseek(file, 0, SEEK_END), where file is the pointer returned by calling fopen).326

> 326) The macro SEEK_END is defined, and the function signatures fopen(const char*, const char*) and fseek(FILE*, long, int) are declared, in <cstdio> (29.12.1).

```
explicit basic_ifstream(const filesystem::path& s,
    ios_base::openmode mode = ios_base::in);
basic_ifstream(const basic_ifstream&) = delete;
basic_ifstream(basic_ifstream&& rhs);

// 29.9.3.3, assign and swap
basic_ifstream& operator=(const basic_ifstream&) = delete;
basic_ifstream& operator=(basic_ifstream&& rhs);
void swap(basic_ifstream& rhs);

// 29.9.3.4, members
basic_filebuf<charT, traits>* rdbuf() const;

bool is_open() const;
void open(const char* s, ios_base::openmode mode = ios_base::in);
void open(const filesystem::path::value_type* s,
    ios_base::openmode mode = ios_base::in);  // wide systems only; see 29.9.1
void open(const string& s, ios_base::openmode mode = ios_base::in);
void open(const filesystem::path& s, ios_base::openmode mode = ios_base::in);
void close();
private:
    basic_filebuf<charT, traits> sb;    // exposition only
};

template<class charT, class traits>
void swap(basic_ifstream<charT, traits>& x,
    basic_ifstream<charT, traits>& y);
```

1 The class basic_ifstream<charT, traits> supports reading from named files. It uses a basic_filebuf<charT, traits> object to control the associated sequence. For the sake of exposition, the maintained data is presented here as:

- (1.1) — sb, the filebuf object.

### 29.9.3.2 Constructors [ifstream.cons]

```
basic_ifstream();
```

1 Effects: Initializes the base class with basic_istream<charT, traits>(addressof(sb)) (29.7.4.2.2) and sb with basic_filebuf<charT, traits>() (29.9.2.2).

```
explicit basic_ifstream(const char* s,
    ios_base::openmode mode = ios_base::in);
explicit basic_ifstream(const filesystem::path::value_type* s,
    ios_base::openmode mode = ios_base::in);  // wide systems only; see 29.9.1
```

2 Effects: Initializes the base class with basic_istream<charT, traits>(addressof(sb)) (29.7.4.2.2) and sb with basic_filebuf<charT, traits>() (29.9.2.2), then calls rdbuf()->open(s, mode | ios_base::in). If that function returns a null pointer, calls setstate(failbit).

```
explicit basic_ifstream(const string& s,
    ios_base::openmode mode = ios_base::in);
explicit basic_ifstream(const filesystem::path& s,
    ios_base::openmode mode = ios_base::in);
```

3 Effects: Equivalent to: basic_ifstream(s.c_str(), mode).

```
basic_ifstream(basic_ifstream&& rhs);
```

4 Effects: Move constructs the base class, and the contained basic_filebuf. Then calls basic_istream<charT, traits>::set_rdbuf(addressof(sb)) to install the contained basic_filebuf.

