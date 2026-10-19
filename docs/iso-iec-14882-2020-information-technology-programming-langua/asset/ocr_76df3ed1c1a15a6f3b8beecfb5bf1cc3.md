```
template<class charT, class traits, size_t N>
    basic_istream<charT, traits>& operator>>(basic_istream<charT, traits>& in, charT (&s)[N]);
template<class traits, size_t N>
    basic_istream<char, traits>& operator>>(basic_istream<char, traits>& in, unsigned char (&s)[N]);
template<class traits, size_t N>
    basic_istream<char, traits>& operator>>(basic_istream<char, traits>& in, signed char (&s)[N]);
```

Effects: Behaves like a formatted input member (as described in 29.7.4.3.1) of in. After a sentry object is constructed, operator>> extracts characters and stores them into s. If width() is greater than zero, n is min(size_t(width()), N). Otherwise n is N. n is the maximum number of characters stored.

Characters are extracted and stored until any of the following occurs:

+   - n-1 characters are stored;
+   - end of file occurs on the input sequence;
+   - letting ct be use_facet<ctype<charT>>(in.getloc()), ct.is(ct.space, c) is true.

operator>> then stores a null byte (charT()) in the next position, which may be the first position if no characters were extracted. operator>> then calls width(0).

If the function extracted no characters, it calls setstate(failbit), which may throw ios_base::failure (29.5.5.4).

Returns: in.

```
template<class charT, class traits>
    basic_istream<charT, traits>& operator>>(basic_istream<charT, traits>& in, charT& c);
template<class traits>
    basic_istream<char, traits>& operator>>(basic_istream<char, traits>& in, unsigned char& c);
template<class traits>
    basic_istream<char, traits>& operator>>(basic_istream<char, traits>& in, signed char& c);
```

Effects: Behaves like a formatted input member (as described in 29.7.4.3.1) of in. After a sentry object is constructed a character is extracted from in, if one is available, and stored in c. Otherwise, the function calls in.setstate(failbit).

Returns: in.

```
basic_istream<charT, traits>& operator>>(basic_streambuf<charT, traits>* sb);
```

Effects: Behaves as an unformatted input function (29.7.4.4). If sb is null, calls setstate(failbit), which may throw ios_base::failure (29.5.5.4). After a sentry object is constructed, extracts characters from *this and inserts them in the output sequence controlled by sb. Characters are extracted and inserted until any of the following occurs:

+   - end-of-file occurs on the input sequence;
+   - inserting in the output sequence fails (in which case the character to be inserted is not extracted);
+   - an exception occurs (in which case the exception is caught).

If the function inserts no characters, it calls setstate(failbit), which may throw ios_base::failure (29.5.5.4). If it inserted no characters because it caught an exception thrown while extracting characters from *this and failbit is set in exceptions() (29.5.5.4), then the caught exception is rethrown.

Returns: *this.

# 29.7.4.4 Unformatted input functions [istream.unformatted]

Each unformatted input function begins execution by constructing an object of class sentry with the default argument noskipws (second) argument true. If the sentry object returns true, when converted to a value of type bool, the function endeavors to obtain the requested input. Otherwise, if the sentry constructor exits by throwing an exception or if the sentry object returns false, when converted to a value of type bool, the function returns without attempting to obtain any input. In either case the number of extracted characters is set to 0; unformatted input functions taking a character array of nonzero size as an argument shall also store a null character (using charT()) in the first location of the array. If an exception is thrown during input then