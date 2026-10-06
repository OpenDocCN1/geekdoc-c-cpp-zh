
# ISO/IEC 14882:2017(E)

```cpp
(4.10)    if (pbase()) pbase() != rhs_a.pbase()
```

```cpp
(4.11)    if (pptr()) ptr() != rhs_a.ptr()
```

```cpp
(4.12)    if (eptr()) eptr() != rhs_a.eptr()
```

```cpp
virtual ~basic_filebuf();
```

5 Effects: Destroys an object of class basic_filebuf<charT, traits>. Calls close(). If an exception occurs during the destruction of the object, including the call to close(), the exception is caught but not rethrown (see 20.5.5.1).

## 30.9.2.2 Assign and swap [filebuf.assign]

```cpp
basic_filebuf& operator=(basic_filebuf& const rhs);
```

1 Effects: Calls close() then moves from rhs. After the move assignment *this is the observable state it would have if it had been constructed from rhs (see 30.9.2.1).

2 Returns: *this.

```cpp
void swap(basic_filebuf& rhs);
```

3 Effects: Exchanges the state of *this and rhs.

```cpp
template <class charT, class traits>
void swap(basic_filebuf<charT, traits>& x,
basic_filebuf<charT, traits>& y);
```

4 Effects: As if x.swap(y).

## 30.9.2.3 Member functions [filebuf.members]

```cpp
bool is_open() const;
```

1 Returns: true if the file was opened to open (returned a non-null value) and there has been no intervening call to close.

```cpp
basic_filebuf* open(const char* s, ios_base::openmode mode);
basic_filebuf* open(const filesystem::path& value_type& s,
ios_base::openmode mode); // wide systems only; see 30.9.1.1
```

2 Effects: If is_open() != false, returns a null pointer. Otherwise, initializes the filebuf as required. If it opens a file, whose name is the NTRS (as by calling open(s, modstr)), the mode is determined from mode ~ios_base::ate as indicated in Table 117. If mode is no combination of flags set it then opens the file.

3 If the open operation succeeds and (mode & ios_base::ate) != 0, positions the file to to the end (as by calling fseek(file, 0, SEEK_END), calls close()).^327

4 If the repositioning operation fails, close() and returns a null pointer to indicate failure.

5 Returns: if successful, a null pointer otherwise.

```cpp
basic_filebuf* open(const string& s, ios_base::openmode mode);
basic_filebuf* open(const filesystem::path& s, ios_base::openmode mode);
```

6 Returns: open(s.c_str(), mode);

> ^327 The macro SEEK_END is defined, and the function signatures open(const char*, const*) and fseek(FILE*, int) are declared, in <cstdio> (30.11.1).

Table 117 — File open modes

| ios_base flag combination | stdio equivalent | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- |
| | | | | + | "w" |
| | | + | + | "a" |
| | | | | + | "ab" |
| | | | | + | "u" |
| + | | | + | "r" |
| + | + | | + | "r+" |
| + | + + | + | "w+" |
| + | | | + | "a+" |
| | | | + | "at" |
| | | | + | "b" |
| | | | + | "ab" |
| | | | + | "wb" |
| + | + | + | "rb" |
| + + + | + | "r+b" |
| + + + | + | "w+b" |
| + + + | + | "a+b" |
| + + + | + | "ab+b" |

basic_filebuf* close();

- 8 *Returns:* On this success, a null pointer otherwise.
- 9 *Postconditions:* is_open() == false.

## 30.9.2.4 Overridden virtual functions [filebuf,virtuals]

streamsize showhowanc() override; basic_streambuf::showhowanc() (30.6.4).

- 1 *Effects:* Behaves as basic_streambuf::showhowanc();
- 2 *Remarks:* An implementation might provide an overriding definition for this function signature if it is determined that more characters can be read from the input sequence.

int_type overflow() override;

- 3 *Effects:* Behaves according to the description of basic_streambuf<charT, traits>::underflow(), with the specialization that a sequence of characters is read from the input sequence as if by reading from the associated file into an internal buffer (extern_buf) and then if by

```cpp
char extern_buf[XSIZE];
```

```cpp
char* extern_end;
char intern_buf[SIZE];
char intern_end;
codecvt_base::result r =
a_codecvt.out(extern_buf, extern_buf+SIZE, extern_end,
    intern_buf, intern_buf+SIZE, intern_end);
```

This shall be done in such a way that the class can recover the position (fpos_t) corresponding to each character between intern_buf and intern_end. If the value of r indicates that a_codecvt() ran out of space in intern_buf, retry with a larger intern_buf.

```cpp
int_type uflow();
```

- 4 | Effects: Behaves according to the description of basic_streambuf<charT>::uflow(), with the specialization that a character is read from the input with the same method as used by underflow.

```cpp
int_type pbackfail(int_type c = traits::eof()) override;
```

- 5 | Effects: Puts back the character designated by c to the input sequence, possible, in one of three ways:
(5.1) If traits::eq_int_type(c, traits::eof()) returns false and if the function makes a putback position available or if traits::to_char(c), gptr()[-1]) returns true, decrements the next pointer for the input sequence, gptr();
Returns: c.
(5.2) If traits::eq_int_type(c, traits::eof()) returns false and if the function makes a putback position available or if the function is permitted to assign to the putback position, decrements the next pointer for the input sequence, stores c there.
Returns: c.
(5.3) If traits::eq_int_type(c, traits::eof()) returns true, and if the input sequence has a putback position available or if the function makes a putback position, decrements the next pointer for the input sequence, gptr();
Returns: c.
- 6 | Returns: not_eof(c).
- 7 | Remarks: If is_open() == false, the function fails.
- 8 | The function can put back a more than one of these ways, it is unspecified.

```cpp
int_type overflow(int_type c = traits::eof()) override;
```

- 10 | Effects: Behaves according to the description of basic_streambuf<charT>::underflow(), with the specialization that a sequence of characters is read from the input sequence as if by reading from the associated file into an internal buffer (extern_buf) and then if by:
```cpp
char* b = pbase();
char* p = pptr();
char* end;
char* inbuf[SIZE];
char* xbuf[SIZE];
codecvt_base::result r =
a_codecvt.out(state, b, p, xbuf, xbuf+SIZE, end);
```
and then if:
(10.1) If r == codecbase::error then fail.
(10.2) If r == codecbase::nocnov then output to the file characters from xbuf (not including) p.
(10.3) If r == codecbase::partial then output to the file characters from xbuf_end, iff output fails.
(10.4) Otherwise de (xbuf not enough) increase SIZE and from the beginning.

- 11 | Returns: traits::not_eof(c) to indicate success, and traits::eof() to indicate failure. If is_open() == false, the function fails.

```cpp
basic_streambuf* setbuf(char_type s, size_t n) override;
```

- 12 Effect: If setbuf is called after any I/O has occurred on that stream, the stream becomes unbuffered. The other results here are implementation-defined. “Unbuffered” means that pbuf and pptr return null and output to the file should appear as soon as possible.

| Way Value | Seek Effects |
| :--- | :--- |
| basic_ios::beg | SEEK_SET |
| basic_ios::cur | SEEK_CUR |
| basic_ios::end | SEEK_END |

-15 Returns: A newly constructed pos_type object that stores the resultant position, if possible. If the positioning operation fails, or the object cannot represent the resultant position, returns pos_type(off_type(-1)).

```cpp
pos_type seekpos(pos_type sp, ios_base::openmode om, = ios_base::in | ios_base::out); override;
 = ios_base::in;
```

- 16 Alters the file position, if possible, to correspond to the position stored in sp (as described below). Altering the file position performs follows:
1. if (om & ios_base::out) != 0, then update the output sequence and return any unset sequence;
2. set the file position to sp as by a call to fsetpos;
3. if (om & ios_base::in) != 0, then update the input sequence;
