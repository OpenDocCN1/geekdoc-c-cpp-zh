
# ISO/14882:2017(E)

explicit sentry(basic_istream<CharT>& is, bool noskipw = false);

Effects: if is.good() is false, calls is.setstate(failbit). Otherwise, prepares for unformatted input. if is.tie() is not a null pointer, calls is.flush() to synchronize the output sequence with any external C stream. Except that this can be suppressed if the input of is.tie() is empty. An implementation is allowed to defer the call until a call of is.rdbuf()->underflow() occurs. If no such occurs before the sentry object is destroyed, the call to flush may be delayed. If noskipw is true and is.flags(), it discards each character as long as the next input character c is a whitespace character. If is.rdbuf()->sbumpc() returns traits::eof(), the function setstate(eofbit) (which may throw ios_base::failure).

- Remarks: The constructor sentry(basic_istream<CharT>&, bool noskipw = false) uses the imbued locale of is, to determine whether the next input character is whitespace or not.

- To decide if c is a whitespace character, the constructor performs as if it executes the following code:
```cpp
typeype<char> ctype = use_facet<ctype<char>>(is.getloc());
if (ctype.space(c) != 0) ok_ = true; else ok_ = false;
// c is a whitespace character.
```

- If, after preparation completes, is.good() is true. During preparation, the constructor may call setstate(failbit) (which may throw ios_base::failure(30.5.5.4))

- -sentry();

Effects: None.

- explicit operator bool();

Effects: Returns ok_.

## 30.7.4.2 Formatted input functions

### 30.7.4.2.1 Common requirements

Each formatted input begins execution by constructing an object of class sentry with the noskipw (second) argument false. If the sentry object returns true, when converted to a value of bool, the function obtains to the requested input. If an exception is thrown during input then ios::badbit is turned on in this's error state. if (exceptions::badbit != 0 then the exception is thrown. In any case, the formatted input function destroys the sentry object. If no exception has been thrown, it returns this.

## 30.7.4.2.2 Arithmetic extractors

```cpp
operator>>(unsigned short& val);
operator>>(unsigned int& val);
operator>>(long& val);
operator>>(unsigned long& val);
```

305 This will be possible only in functions that are part of the library. The semantics of the constructor used in user code is as specified.

306 The sentry constructor and destructor can also perform additional implementation-dependent operations.

307 This is without causing an ios::failure to be thrown.

operator>>(long long& val);
operator>>(unsigned long long& val);
operator>>(float& val);
operator>>(double& val);
operator>>(long double& val);
operator>>(bool& val);
operator>>(void& val);

- In the case of the inserters, these extractors extract the private member of the locale's num_get<> (25.4.2.1) object to perform parsing the input stream data. These extractors behave as formatted input functions (as is described in 30.7.4.2). After a sent object is constructed, the conversion occurs as if performed by the following code:

```cpp
using num_get_char<char, istream_iterator<char, traits>>;
iostate err = iostate::goodbit;
use_get<numeric>(loc).get(*this, 0, *this, err, lval);
setstate(err);
```

In the above fragment, loc stands for the basic_ios_class. [Note: The first argument provides an object of the istream_iterator class which is an iterator pointed to an input stream. It bypasses itream and uses streambufs. — end note] Locale relies on this type as interface to istream, so that it does not depend directly on istream.

operator>>(int& val);
The conversion occurs as if performed by the following code fragment (using the same notation as for the preceding code):

```cpp
using num_get_char<char, istream_iterator<char, traits>>;
iostate err = ios_base::goodbit;
long lval;
use_get<numeric>(loc).get(*this, 0, *this, err, lval);
if (lval < numeric_limits<int>::min())
 err = ios_base::failbit;
val = numeric_limits<int>::min();
else if (lval > numeric_limits<int>::max() < lval)
 err = ios_base::failbit;
val = numeric_limits<int>::max();
else
val = static_cast<short>(lval);
setstate(err);
```

```cpp
val = static_cast<int>(lval);
setstate(basic_istream::err);
```

## 30.7.4.2.3 basic_istream::operator>

```cpp
basic_charT, traits&*operator=(basic_istream<charT, traits&> (*pf)(basic_istream<charT, traits&));
```

Effects: None. This extractor does not behave as a formatted input function (as described in 30.7.4.2.1)

Returns: pf(*this).

```cpp
basic_charT, traits&*operator=(basic_ios<charT, traits&> (*pf)(basic_ios<charT, traits&));
```

Effects: pf(*this). This extractor does not behave as a formatted input function (as described in 30.7.4.2.1).

Returns: *this.

```cpp
basic_charT, traits&*operator=(ios_base& (*pf)(ios_base&));
```

Effects: pf(*this). This extractor does not behave as a formatted input function (as described in 30.7.4.2.1).

Returns: *this.

```cpp
template<class charT>
basic_istream<charT, traits&>&operator>(in, charT& s);
template<class charT>
basic_istream<charT, traits&>&operator>(in, unsigned charT& s);
template<class charT>
basic_istream<charT, traits&>&operator>(in, signed charT& s);
``` (Wait, the original text has some overlaps here)

Effects: Behaves as a formatted input function (as described in 30.7.4.2.1). After a sentry object is constructed, it extracts characters and stores them into successive locations of an array whose element is designated by s. If width() is greater than zero, n is width(). Otherwise n is the maximum number of characters stored. n is the maximum number of characters of char_type that can store a terminating char(). Characters are extracted and stored until any of the following:

- n-1 characters are stored;
- end of file on the input sequence;
- letting ce store a null byte in the next (in.get()), ct.is(), is true.
- operator then sets width(0)

If the extraction fails, it calls setstate(failbit), which may trigger ios_base::failure(30.5.5.4)

Returns: in.

```cpp
template<class charT, traits&>&operator=(basic_istream<charT, traits&>& in, charT& c);
```

308 See, for example, the function ws(30.7.4.4).
309 See, for example, the function dec(ios_base)(30.5.6.3).

- 12 Effects: As a formatted input member (as described in 30.7.4.2.1) of in. If a sentry object is constructed from it, if in is also valued, and stored in c. Otherwise, function calls setstate(failbit).
- 13 Returns: in.
- 14 Effects: As an unformatted input function (30.7.4.3). If sb is null, calls setstate(failbit), which may throw ios_base::failure(30.5.5.4). After a sentry object is constructed, extracts characters from and inserts them into the output sequence controlled by sb. Characters extracted and inserted until the end of input

- (14.1) end-of-file sequence
- (14.2) inserting into the output sequence fails (in case the character to be inserted is not extracted)
- (14.3) an exception occurs (in case the exception is caught).

If the function cannot, it calls setstate(failbit), which may throw ios_base::failure (30.5.5.4) if it cannot extract because it catches an exception while throwing characters from*this and failbit is turned on in*this error state. (Exceptions from basic_ios::clear()) not caught or rethrown). If (exceptions()&badbit != 0 then the exception is rethrown. It counts the number of characters extracted. If no exception has been thrown it ends by storing the count in a object and returning the value. In any case the sentry is destroyed before leaving the unformatted input function.

- 16 Returns: this.

## 30.7.4 Unformatted input functions

1 Each unformatted input begins execution by constructing an object of sentry with return, when converted to a type bool, the constructor proceeds to obtain the requested input. If the sentry object returns true, when converted. Otherwise, if the sentry constructor exists by throwing an exception if the sentry object returns fails, converted to a value of type bool, function returns without invalidating any input. In either case the number of characters extracted is set to the value of the input function taking the maximum size as an argument. If it reads a character (char*) in the first location of or. If an exception occurs during input then ios::badbit is turned on in this error state. (Exceptions from basic_ios::clear()) not caught or rethrown). If (exceptions()&badbit != 0 then the exception is rethrown. It counts the number of characters extracted. If no exception has been thrown it ends by storing the count in a object and returning the value. In any case the sentry is destroyed before leaving the unformatted input function.

- 2 Effects: None. This member function does not behave as an unformatted input function (as described).
- 3 Returns: The number of characters extracted by the last unformatted input member function called the object.

```cpp
int_type get();
```

- 4 Effects: As an unformatted input function (as described above). After constructing a sentry object, extracts a character c, if one is available. Otherwise, the function calls setstate(failbit), which may throw ios_base::failure(30.5.5.4).
