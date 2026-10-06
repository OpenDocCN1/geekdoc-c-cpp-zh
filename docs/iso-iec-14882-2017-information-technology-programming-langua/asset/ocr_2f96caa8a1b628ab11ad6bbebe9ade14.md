# ISO/IEC 14882:2017(E)

(25.1) — n : numeric_limits<streamsize>::max() (21.3.4) and n characters have been extracted far

(25.2) — end-file occurs on the input sequence (in which the function calls setstate(eof), which may throw through ios_base::failure (30.5.5.4));

(25.3) — traits::eq_int_type(traits::to_int_type(c), delim) for the next available input character c (in which c is extracted).

26 Remarks: The last value will never occur if traits::eq_int_type(delim, traits::eof()).

27 — *this.

# int_type peek();

28 Effects: Behaves as an unformatted input function (as described above). After constructing a sentry object, does not extract the current character.

29 Returns: traits::eof() if it is false. Otherwise, returns rdbuf()->get().

```
basic_istream<charT, traits>& read(charT* s, streamsize n);
```

30 Effects: Behaves as an unformatted input function (as described above). After constructing a sentry object, if good() calls setstate(failbit) which may throw an exception, and return. Otherwise extracts characters and stores them into successive locations of an array whose first element is defined by s.317 Characters are extracted until one of the following:

+   (30.1) — n characters are stored;

+   (30.2) — end-file occurs on the input sequence (in which the function calls setstate(failbit | eof), which may throw ios_base::failure(30.5.5.4));

31 — *this.

```
streamsize read(charT* s, streamsize n);
```

32 Effects: Behaves as an unformatted input function (as described above). After constructing a sentry object, if good() calls setstate(failbit) which may throw an exception, and return. Otherwise extracts characters and stores them into successive locations of an array whose first element is designated by s. If rdbuf()->in_avail() == -1, calls setstate(eof) (which may throw ios_base::failure(30.5.5.4)), and extracts no characters;

+   (32.1) — If rdbuf()->in_avail() == 0, extracts no characters

+   (32.2) — If rdbuf()->in_avail() > 0, extracts min(rdbuf()->in_avail(), n)).

33 Returns: The number of characters extracted.

```
basic_istream<charT, traits>& putback(charT c);
```

34 Effects: Behaves as an unformatted input function (as described above), except that the function clears EOF. After constructing a sentry object, if good() calls setstate(failbit) which may throw an exception, and return. If good(), rdbuf()->putback(c). If putback returns traits::badbit() (which may throw ios_base::failure(30.5.5.4)). [Note: This extracts no characters, so the value returned by the next call to get() is 0.] — *end line*

35 — *this.

```
basic_istream<charT, traits>& unset();
```

30 Effects: Behaves as an unformatted input function (as described above), except that the function is not overloaded over signed char and unsigned char.

37 Note that this function is not overloaded over signed char and unsigned char