# ISO/IEC 14882:2017(E)

functions enable path support for systems with a wide path character type, such as wchar_t.— end node];

# 30.9.2 Class template basic_filebuf [filebuf]

```
namespace std {
template <class Char, class traits = char_traits<Char>>
basic_filebuf : public basic_streambuf<Char, traits> {
public:
    using char_type = Char;
    using int_type = typename traits::int_type;
    using pos_type = typename traits::pos_type;
    using off_type = typename traits::off_type;
    using traits_type = traits;

    basic_filebuf() const;
    basic_filebuf(const basic_filebuf& rhs) = delete;
    basic_filebuf(basic_filebuf&& rhs) = noexcept;
    virtual ~basic_filebuf();
```

### 30.9.2.1. constructors/destructor

```
basic_filebuf& operator=(const basic_filebuf& rhs) = delete;
basic_filebuf& operator=(basic_filebuf&& rhs) = noexcept;
void swap(basic_filebuf& rhs);
```

### 30.9.2.2. assignment and swap

```
basic_filebuf& operator=(const basic_filebuf& rhs) = delete;
basic_filebuf& operator=(basic_filebuf&& rhs) = noexcept;
void swap(basic_filebuf& rhs);
```

### 30.9.2.3.

```
bool is_open() const;
basic_filebuf* open(const char* s, ios_base::openmode mode);
basic_filebuf* open(const filesystem::path::value_type& s, // wide characters only; see 30.9.1
    ios_base::openmode mode);
basic_filebuf* open(const std::string& s,
    ios_base::openmode mode);
basic_filebuf* open(const filesystem::path& s,
    ios_base::openmode mode);
basic_filebuf* close();
```

protected:

### 30.9.2.4. overridden virtual functions

```
string showmanyc() override;
int_type underflow() override;
int_type overflow() override;
int_type syncback(int_type c = traits::eof()) override;
int_type overflow(int_type c = traits::eof()) override;
```

```
basic_streambuf<Char, traits>* setbuf(char_type s,
    streamsize n) override;
pos_type seekoff(off_type off, ios_base::seekdir dir,
    ios_base::openmode mode)
    = ios_base::in | ios_base::out) override;
pos_type seekpos(pos_type sp,
    ios_base::openmode mode)
    = ios_base::in | ios_base::out) override;
int
    ync() override;
imimbue(const locale& loc) override;
```

```
};
```