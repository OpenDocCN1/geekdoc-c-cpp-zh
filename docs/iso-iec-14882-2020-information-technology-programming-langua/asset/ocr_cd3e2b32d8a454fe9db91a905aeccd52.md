# 29.9.3.3  Assignment and swap

`void swap(basic_ifstream& rhs);`

*Effects:* Exchanges the state of `*this` and `rhs` by calling `basic_istream<charT, traits>::swap(rhs)` and `sb.swap(rhs.sb)`.

```
template<class charT, class traits>
    void swap(basic_ifstream<charT, traits>& x,
              basic_ifstream<charT, traits>& y);
```

*Effects:* Equivalent to: `x.swap(y)`.

# 29.9.3.4  Member functions

`basic_filebuf<charT, traits>* rdbuf() const;`

*Returns:* `const_cast<basic_filebuf<charT, traits>*>(addressof(sb))`.

`bool is_open() const;`

*Returns:* `rdbuf()->is_open()`.

```
void open(const char* s, ios_base::openmode mode = ios_base::in);
void open(const filesystem::path& s, value_type* s,
          ios_base::openmode mode = ios_base::in);  // wide systems only; see 29.9.1
```

*Effects:* Calls `rdbuf()->open(s, mode | ios_base::in)`. If that function does not return a null pointer calls `clear()`, otherwise calls `setstate(failbit)` (which may throw `ios_base::failure`) (29.5.5.4).

```
void open(const string& s, ios_base::openmode mode = ios_base::in);
void open(const filesystem::path& s, ios_base::openmode mode = ios_base::in);
```

*Effects:* Calls `open(s.c_str(), mode)`.

```
void close();
```

*Effects:* Calls `rdbuf()->close()` and, if that function returns a null pointer, calls `setstate(failbit)` (which may throw `ios_base::failure`) (29.5.5.4).

# 29.9.4  Class template basic_ofstream

# 29.9.4.1  General

```
namespace std {
    template<class charT, class traits = char_traits<charT>>
    class basic_ofstream : public basic_ostream<charT, traits> {
    public:
        using char_type   = charT;
        using int_type    = typename traits::int_type;
        using pos_type    = typename traits::pos_type;
        using off_type    = typename traits::off_type;
        using traits_type = traits;

        // 29.9.4.2, constructors
        basic_ofstream();
        explicit basic_ofstream(const char* s,
                                ios_base::openmode mode = ios_base::out);
        explicit basic_ofstream(const filesystem::path::value_type* s,
                                ios_base::openmode mode = ios_base::out);
        explicit basic_ofstream(const string& s,
                                ios_base::openmode mode = ios_base::out);
        explicit basic_ofstream(const filesystem::path& s,
                                ios_base::openmode mode = ios_base::out);
        basic_ofstream(const basic_ofstream&) = delete;
        basic_ofstream(basic_ofstream&& rhs);

        // 29.9.4.3, assign and swap
        basic_ofstream& operator=(const basic_ofstream&) = delete;
```