
## ISO/IEC 14882:2020(E)

**Table 116: fmtflags effects [tab:ios.fmtflags]**

| Element | Effect(s) if set |
| --- | --- |
| boolalpha | insert and extract bool type in alphabetic format |
| dec | converts integer input or generates integer output in decimal base |
| fixed | generate floating-point output in fixed-point notation |
| hex | converts integer input or generates integer output in hexadecimal base |
| internal | adds fill characters at a designated internal point in certain generated output, or identical to right if no such point is designated |
| left | adds fill characters on the right (final positions) of certain generated output |
| oct | converts integer input or generates integer output in octal base |
| right | adds fill characters on the left (initial positions) of certain generated output |
| scientific | generates floating-point output in scientific notation |
| showbase | generates a prefix indicating the numeric base of generated integer output |
| showpoint | generates a decimal-point character unconditionally in generated floating-point output |
| showpos | generates a + sign in non-negative generated numeric output |
| skipws | skips leading whitespace before certain input operations |
| unitbuf | flushes output after each output operation |
| uppercase | replaces certain lowercase letters with their uppercase equivalents in generated output |

**Table 117: fmtflags constants [tab:ios.fmtflags.const]**

| Constant | Allowable values |
| --- | --- |
| adjustfield | `left`, `right`, `internal` |
| basefield | `dec`, `oct`, `hex` |
| floatfield | `scientific`, `fixed` |

**Table 118: iostate effects [tab:ios.iostate]**

| Element | Effect(s) if set |
| --- | --- |
| badbit | indicates a loss of integrity in an input or output sequence (such as an irrecoverable read error from a file); |
| eofbit | indicates that an input operation reached the end of an input sequence; |
| failbit | indicates that an input operation failed to read the expected characters, or that an output operation failed to generate the desired characters. |

**Table 119: openmode effects [tab:ios.openmode]**

| Element | Effect(s) if set |
| --- | --- |
| app | seek to end before each write |
| ate | open and seek to end immediately after opening |
| binary | perform input and output in binary mode (as opposed to text mode) |
| in | open for input |
| out | open for output |
| trunc | truncate an existing stream when opening |

**Table 120: seekdir effects [tab:ios.seekdir]**

| Element | Meaning |
| --- | --- |
| beg | request a seek (for subsequent input or output) relative to the beginning of the stream |
| cur | request a seek relative to the current position within the sequence |
| end | request a seek relative to the current end of the sequence |

### 29.5.3.2.6 Class ios_base::Init

```cpp
namespace std {
  class ios_base::Init {
  public:
    Init();
    Init(const Init&) = default;
    ~Init();
    Init& operator=(const Init&) = default;
  private:
    static int init_cnt;      // exposition only
  };
}
```

1 The class `Init` describes an object whose construction ensures the construction of the eight objects declared in `<iostream>` (29.4) that associate file stream buffers with the standard C streams provided for by the functions declared in `<cstdio>` (29.12.1).

2 For the sake of exposition, the maintained data is presented here as:

- (2.1) — `static int init_cnt`, counts the number of constructor and destructor calls for class `Init`, initialized to zero.

`Init();`

3 Effects: Constructs and initializes the objects `cin`, `cout`, `cerr`, `clog`, `wcin`, `wcout`, `wcerr`, and `wclog` if they have not already been constructed and initialized.

`~Init();`

4 Effects: If there are no other instances of the class still in existence, calls `cout.flush()`, `cerr.flush()`, `clog.flush()`, `wcout.flush()`, `wcerr.flush()`, `wclog.flush()`.

### 29.5.3.3 State functions

`fmtflags flags() const;`

1 Returns: The format control information for both input and output.

`fmtflags flags(fmtflags fmtfl);`

2 Postconditions: `fmtfl == flags()`.

3 Returns: The previous value of `flags()`.

`fmtflags setf(fmtflags fmtfl);`

4 Effects: Sets `fmtfl` in `flags()`.

5 Returns: The previous value of `flags()`.

`fmtflags setf(fmtflags fmtfl, fmtflags mask);`

6 Effects: Clears `mask` in `flags()`, sets `fmtfl & mask` in `flags()`.

7 Returns: The previous value of `flags()`.

`void unsetf(fmtflags mask);`

8 Effects: Clears `mask` in `flags()`.

`streamsize precision() const;`

9 Returns: The precision to generate on certain output conversions.

`streamsize precision(streamsize prec);`

10 Postconditions: `prec == precision()`.

### 29.5.3.4 Functions [ios.base.locales]

`streamsize width(streamsize wide);`

Postconditions: `wide == width()`.

Returns: The previous value of `width()`.

`locale imbue(const locale& loc);`

Effects: Calls each registered callback pair (`fn`, `idx`) (29.5.3.7) as `(*fn)(imbue_event, *this, idx)` at such a time that a call to `ios_base::getloc()` from within `fn` returns the new locale value `loc`.

Postconditions: `loc == getloc()`.

Returns: The previous value of `getloc()`.

`locale getloc() const;`

Returns: If no locale has been imbued, a copy of the global C++ locale, `locale()`, in effect at the time of construction. Otherwise, returns the imbued locale, to be used to perform locale-dependent input and output operations.

### 29.5.3.5 Static members [ios.members.static]

`static bool sync_with_stdio(bool sync = true);`

Returns: `true` if the previous state of the standard iostream objects (29.4) was synchronized and otherwise returns `false`. The first time it is called, the function returns `true`.

Effects: If any input or output operation has occurred using the standard streams prior to the call, the effect is implementation-defined. Otherwise, called with a `false` argument, it allows the standard streams to operate independently of the standard C streams.

When a standard iostream object `str` is synchronized with a standard stdio stream `f`, the effect of inserting a character `c` by `fputc(c, f)` is the same as the effect of `str.rdbuf()->sputc(c)` for any sequences of characters; the effect of extracting a character `c` by `c = fgetc(f)` is the same as the effect of `c = str.rdbuf()->sbumpc()` for any sequences of characters; and the effect of pushing back a character `c` by `ungetc(c, f)` is the same as the effect of `str.rdbuf()->sputbackc(c)` for any sequence of characters.291

> 291) This implies that operations on a standard iostream object can be mixed arbitrarily with operations on the corresponding stdio stream. In practical terms, synchronization usually means that a standard iostream object and a standard stdio object share a buffer.

### 29.5.3.6 Storage functions [ios.base.storage]

`static int xalloc();`

Returns: `index++`.

Remarks: Concurrent access to this function by multiple threads does not result in a data race (6.9.2).

`long& iword(int idx);`

Preconditions: `idx` is a value obtained by a call to `xalloc`.

Effects: If `iarray` is a null pointer, allocates an array of `long` of unspecified size and stores a pointer to its first element in `iarray`. The function then extends the array pointed at by `iarray` as necessary.

### 29.5.4.1 Members [fpos.members]

`void state(stateT s);`

1 Effects: Assigns `s` to `st`.

`stateT state() const;`

2 Returns: Current value of `st`.

### 29.5.4.2 Requirements [fpos.operations]

1 An `fpos` type specifies file position information. It holds a state object whose type is equal to the template parameter `stateT`. Type `stateT` shall meet the `Cpp17DefaultConstructible` (Table 27), `Cpp17CopyConstructible` (Table 29), `Cpp17CopyAssignable` (Table 31), and `Cpp17Destructible` (Table 32) requirements. If `is_trivially_copy_constructible_v<stateT>` is true, then `fpos<stateT>` has a trivial copy constructor. If `is_trivially_copy_assignable_v<stateT>` is true, then `fpos<stateT>` has a trivial copy assignment operator. If `is_trivially_destructible_v<stateT>` is true, then `fpos<stateT>` has a trivial destructor. All specializations of `fpos` meet the `Cpp17DefaultConstructible`, `Cpp17CopyConstructible`, `Cpp17CopyAssignable`, `Cpp17Destructible`, and `Cpp17EqualityComparable` (Table 25) requirements. In addition, the expressions shown in Table 121 are valid and have the indicated semantics. In that table,

- (1.1) — `P` refers to an instance of `fpos`,
- (1.2) — `p` and `q` refer to values of type `P` or `const P`,
- (1.3) — `p1` and `q1` refer to modifiable lvalues of type `P`,
- (1.4) — `O` refers to type `streamoff`, and
- (1.5) — `o` refers to a value of type `streamoff` or `const streamoff`.

**Table 121: Position type requirements [tab:fpos.operations]**

| Expression | Return type | Operational semantics | Assertion/note pre-/post-condition |
| --- | --- | --- | --- |
| `P(o)` | `P` | converts from offset | Effects: Value-initializes the state object. |
| `P p(o); P p = o;` |  |  | Effects: Value-initializes the state object. Postconditions: `p == P(o)` |
| `P()` | `P` | `P(0)` |  |
| `P p;` |  | `P p(0);` |  |
| `O(p)` | `streamoff` | converts to offset | `P(O(p)) == p` |
| `p != q` | convertible to `bool` | `!(p == q)` |  |
| `p + o` | `P` | + offset | Remarks: With `q1 = p + o;`, then: `q1 - o == p` |
| `p1 += o` | `P&` | += offset | Remarks: With `q1 = p1;` before the `+=`, then: `p1 - o == q1` |
| `p - o` | `P` | - offset | Remarks: With `q1 = p - o;`, then: `q1 + o == p` |
| `p1 -= o` | `P&` | -= offset | Remarks: With `q1 = p1;` before the `-=`, then: `p1 + o == q1` |
| `o + p` | convertible to `P` | `p + o` | `P(o + p) == p + o` |
| `p - q` | `streamoff` | distance | `p == q + (p - q)` |

2 Stream operations that return a value of type `traits::pos_type` return `P(O(-1))` as an invalid value to signal an error. If this value is used as an argument to any `istream`, `ostream`, or `streambuf` member that accepts a value of type `traits::pos_type` then the behavior of that function is undefined.
