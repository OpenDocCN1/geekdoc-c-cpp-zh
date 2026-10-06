# ISO/IEC 14882:2017(E)

```
void swap(basic_ios& rhs) noexcept;
```

Effects: The states of *this and rhs shall be exchanged, except rdbuf() shall return the same value as it returned before the call, and rdbuf() shall return the same value as it returned before the call.

```
void set_rdbuf(basic_streambuf<char, traits**> sb);
```

```
sb! != nullptr;
```

Effects: Associates the basic_streambuf object pointed to sb by this stream without calling clear().

Postconditions: rdbuf() == sb.

Throws: Nothing.

# 30.5.5.4 basic_ios flags functions [iostate.flags]

```
explicit operator bool() const;
```

Returns: !fail().

```
bool operator!() const;
```

Returns: fail().

```
iostate rstate() const;
```

Returns: The error of the stream buffer.

```
void clear(iostate state = goodbit);
```

Postconditions: If rdbuf() != 0 then rstate(); otherwise rstate() == (state | ios_base::badbit).

Effects: If ((state | (rdbuf() ? goodbit : badbit)) & exceptions()) == 0, Otherwise, the function throws an object of basic_ios::failure (30.5.3.1.1), constructed with implementation-defined argument values.

```
void rstate(iostate state);
```

Effects: Calls clear(rstate() | state) (which may throw basic_ios::failure (30.5.3.1.1)).

```
bool good() const;
```

Returns: rstate() == 0

```
bool eof() const;
```

Returns: true if eof is set in rstate().

```
bool fail() const;
```

Returns: true if failbit or badbit is set in rstate().297

```
bool bad() const;
```

Returns: true if badbit is set in rstate().

```
iostate exceptions() const;
```

Returns: A mask that determines what elements is set in rstate() cause exceptions to be thrown.

> 297) Checking badbit also for fail() is historical practice.