
# ISO/IEC 14882:2017(E)

## Table 107 — fmtflags effects

| Element | Effect(s) if set |
| --- | \--- |
| boolalpha | insert and extract bool type in alphabetical format |
| dec | converts integer input or generates output in decimal base |
| fixed | generates floating-point output in fixed-point notation |
| hex | converts integer input or generates integer output in hexadecimal base |
| internal | adds fill characters to designated integer point in certain output, or identical to right if no such is designated |
| left | adds fill characters on the right (final positions) of certain generated output |
| oct | converts integer input or generates output in octal base |
| right | adds fill characters on the left (initial positions) of certain generated output |
| scientific | generates floating-point output in scientific notation |
| showbase | generates a prefix indicating the numeric base of generated output |
| showpoint | generates a decimal-point character unconditionally in generated floatingpoint output |
| showpos | generates a sign in non-negative numeric output |
| skipws | keeps leading whitespace before before operation |
| unitbuf | flushes output after each output operation |
| uppercase | replaces lowercase letters with their uppercase equivalents in generated output |

## Table 108 — fmtflags constants

| Constant | Allowable values |
| --- | --- |
| adjustfield | left | right | internal |
| basefield | dec | oct | hex |
| floatfield | scientific | fixed |

## Table 109 — iostate effects

| Element | Effect(s) if set |
| --- | --- |
| badbit | indicates a loss of integrity in an input or output sequence (such as an error read from a file); |
| eofbit | indicates that an input operation reached the end of an input sequence; |
| failbit | indicates that an input operation failed to read the expected characters, or that an output operation failed to generate the desired characters. |

## Table 110 — openmode effects

| Element | Effect(s) if set |
| --- | --- |
| app | seek to end before each read |
| ate | open and seek to end immediately after opening |
| binary | perform input and output in binary mode (as opposed to text mode) |
| in | open for input |
| out | open for output |
| trunc | truncate an existing stream when opening |

## Table 111 — seekdir effects

| Element | Meaning |
| --- | --- |
| beg | request a seek (for subsequent input or output) relative to the beginning of the stream |
| cur | request a seek relative to the current position within the sequence |
| end | request a seek relative to the current end of the sequence |

### 30.5.3.1.6 Class ios_base::Init

```cpp
namespace std {
class ios_base::Init {
public:
    Init();
    ~Init();
private:
    static int init_cnt; // exposition only
};
}
```

The Class Init describes an object whose constructor describes the construction of the eight objects declared in `<iostream>` (30.4) that associate file streams with the standard C streams provided by the functions declared in `<cstdio>` (30.11.1).

For the sake of exposition, the maintained data is presented here:

- (2.1) static int init_cnt, counts the number of constructor and destructor calls for class Init, initialized to zero.

```cpp
Init();
```

- Effects: Constructs an object of class Init. It counts and initializes the objects cin, cout, cerr, clog.flush(), cerr.flush(), clog.flush(), wout.flush(), wcerr.flush(), wlog.flush() if they have not already been constructed and initialized.

```cpp
~Init();
```

- Effects: Destroys an object of class Init. If there are no other instances of the class still in existence, calls cout.flush(), cerr.flush(), clog.flush(), wout.flush(), wcerr.flush(), wlog.flush().

### 30.5.3.2 ios_base state functions

```cpp
int fflags() const;
```

- Returns: The format information for input and output.

```cpp
int fflags(int flags);
```

- Postconditions: fmtfl == fflags().

```cpp
void setffags(int fmtfl);
```

- Returns: The previous value of fflags().

```cpp
void setffags(int fmtfl, int mask);
```

- Effects: Clears mask in flags(), sets fmtfl & mask in flags().

```cpp
void unsetf(intflag mask);
```

- Effects: Clears mask in flags().

```cpp
streamsize precision() const;
```

- Returns: The precision to generate on certain conversions.

```cpp
streamsize precision(streamsize prec);
```

- Postconditions: re == precision().

- Returns: The previous value of precision().

```cpp
streamsize width() const;
```

- Returns: The minimum field width (number of characters) to generate on certain conversions.

```cpp
streamsize width(streamsize w);
```

- Postconditions: wide == width().

- Returns: The previous value of width().

### 30.5.3.3 ios_base functions [ios.base.locales]

```cpp
locale imbue(const locale& loc);
```

- Effects: Each registered callback (fn, index) (30.5.3.6) as (*fn) (imbue_event, *this, index) at a time that a call to ios_base::getloc() from within fn returns the new locale. Returns the previous value of loc().

- Postconditions: loc == getloc().

- Returns: If no locale has been imbued, copy of the global C++ locale(loc), at the time of construction. Otherwise, returns the imbued locale, to perform locale-dependent input and output operations.

### 30.5.3.4 ios_base static members [ios.members.static]

```cpp
bool sync_with_stdio(bool sync = true);
```

- Returns: If the previous state of iostream objects (30.4) was synchronized and otherwise returns false. The first time it is, the function returns true.

- Effects: If any input or output operation has occurred the standard streams prior to the call, the implementation is implementation-defined. Otherwise, with a false argument, it allows the standard streams to operate independently of the standard streams.

- When a standard iostream object str is synchronized with a standard std f, the effect of inserting a character by `fputc(f, c)` is the same as the effect of `str.rdbuf()->put(c)` for any sequences of characters; the effect of extracting a character `c = fgetc(f)` is as the effect of `c = str.rdbuf()->sdbpc` for any sequences of characters; and the effect of pushing back character by `getc(c, f)` is as the effect of `str.rdbuf()->putbackc(c)` for any sequence of characters.

### 30.5.3.5 ios_base storage functions [ios.base.storage]

```cpp
static int calloc();
```

- Returns: index++.
- Remarks: Concurrent access to this function by multiple threads shall not result in a data race (4.7).

```cpp
long iword(int idx);
```

- Effects: If is a null pointer, it allocates an array of long unspecified size and stores a pointer to its first element in iarray. The function then extends the array pointed by iarray as necessary to include the element iarray[idx]. Newly allocated element of the array is initialized to zero. The reference returned is invalid after any operations on the object. However, if the function fails and this is a base subclass of a basic_io object or object, the effect is equivalent to calling basic_ios::setstate(badbit) on the derived object (which may throw failure).
- Returns: iarray[idx] initialized to 0.

```cpp
void* pword(int idx);
```

- Effects: If a null pointer, it allocates an array of pointers to void of unspecified size and stores a pointer to its first element in array. The function then extends the array pointed by array as necessary to include the element array[idx]. Newly allocated element of the array is initialized to zero, the value with the same index yields another reference to the same value. If the function fails and this is a base subclass of a basic_io object or object, the effect is equivalent to calling basic_ios::setstate(badbit) on the derived object (which may throw failure). The reference of the storage referred to is retained, so until the next call to copyfmt, pword with the same index yields another reference to the same value.
- Returns: On success array[idx]. A valid void* initialized to 0.
- Remarks: After a subsequent call to pword(int) for the same object, the earlier return value may no longer be valid.

> 250 This implies that operates on a standard iostream stream can be mixed with operations on the corresponding stdio stream. In practical terms, synchronization usually means that a standard iostream and a standard stdio object share a buffer.

> 293 Implementation is free to implement the integer array pointed at by iarray and the pointer array pointed at by array as data structures, possibly with a one-element cache for each.

> 294 For example, because it cannot allocate space.

> 295 For example, because it cannot allocate space.
