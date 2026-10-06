
# ISO/IEC 14882:2017

5 Returns: c if available, otherwise traits::eof().

basic_istream<char, traits&>&get(char* c);
6 Effects: Behaves as an unformatted input (as described above). After constructing a sentry object, extracts a character, if it is available, and assigns to c. 9 Otherwise, the function calls setstate(failbit) (which may throw ios_base::failure(30.5.5.4)).
7 Returns: *this.

basic_istream<char, traits&>&get(char* s, size_t n, char delim);
8 Effects: Behaves as an unformatted input (as described above). After constructing a sentry object, extracts characters and stores them into sequence locations of anywhere first element is defined by s. Characters are extracted and stored until any of the following occurs:

- (8.1) n is less than one or n characters are stored;
- (8.2) end-of-file occurs on the input sequence (in which case the function calls setstate(eof));
- (8.3) traits::eq(c, delim) for the next available input character c (in which case c is not extracted);

9 If the function has no characters, it calls setstate(failbit) (which may throw ios_base::failure(30.5.5.4)). In any case, if n is greater than zero it inserts a null character into the next successive location of the array.
10 Returns: *this.

basic_istream<char, traits&>&get(char* s, size_t n);
11 Effects: Gets(s, n, width('\n')).
12 Returns: Value returned by the call.

basic_istream<char, traits&>&get(char* sb, char delim);
13 Effects: Behaves as an unformatted input (as described above). After constructing a sentry object, extracts characters and inserts them in the output sequence controlled by sb. Characters are extracted and inserted until any of the following occurs:

- (13.1) end-of-file occurs on the input sequence;
- (13.2) inserting into the output sequence (in which case the character to be inserted is not extracted);
- (13.3) traits::eq(c, delim) for the next available input character c (in which case c is not extracted);
- (13.4) an exception occurs (in which case the exception is caught but not rethrown).

14 If the function has no characters, it calls setstate(failbit) (which may throw ios_base::failure(30.5.5.4)).
15 Returns: *this.

basic_istream<char, traits&>&get(char_type s, traits&>& sb);
16 Effects: Gets(sb, width('\n')).
17 Returns: Value returned by the call.

basic_istream<char, traits&>&getline(char_type* s, size_t n, char delim);
18 Effects: Behaves as an unformatted input (as described above). After constructing a sentry object, extracts characters and stores them into sequence locations of anywhere first element is designated by s.

Note that this function is not overloaded on signed char and unsigned char.

# ISO/IEC 14882:2017(E)

Characters are extracted and stored until one of the following occurs:

- 1. end-of-file occurs on the input sequence (in which case the function calls setstate(eofbit));
- 2. traits::eq(c, delim) for the next available input character c (in which case the input character is extracted but not stored).
- 3. n is less than one or an n - 1 characters are stored (in which case the function calls setstate(failbit)).

These conditions are tested in the order shown.

If the function extracts no characters, it calls setstate(failbit) (which may throw ios_base::failure(30.5.4)).

In any case, if n is greater than zero, it stores a null character (using charT()) into the next successive location of the array.

Returns: *this.

[Example]

```cpp
#include <iostream>

int main() {
    using namespace std;
    const int buffer_size = 100;

    char buffer[line_buffer_size];
    int line_number = 0;
    while (cin.getline(buffer, line_buffer_size, '\n') || cin.get()) {
        int count = cin.gcount();
        if (cin.eof())
        else if (cin.fail()) {
            cout << "Partial final line"; // cin.fail() is false
            cout << "Partial long line";
            cin.clear(cin.rdstate() & ~ios_base::failbit);
        } else {
            count--; // Don't include newline in count
            cout << "Line " << line_number << ":" << buffer << endl;
        }
    }
    cout << " " << count << " chars: " << buffer << endl;
}
```
[end example]

basic_istream<char,traits&>&get(char_type* s, istream& n, char* s)
Returns: get(s, n, widen(n = 1, int_type delim = traits::eof()));
Effects: Behaves as an unformatted input (as described above). After constructing a sentry object, extracts and discards them. Characters are extracted until one of the following occurs:

Note that this function is not overloaded on signed char and unsigned char. Since the final input character is "extracted", it is counted in gcount(), even though it is not stored. This allows an input line which exactly fills the buffer, without setting failbit. This is different than historical implementation. This implies an empty input line will not cause fail to be set.

- (1) n is numeric_limits<streamsize>::max() and
- (2) end-of-file occurs on the input sequence (in which case the function calls setstate(eof), which may throw ios_base::failure(30.5.5.4));
- (3) traits::eq_type(c, delim) for the next available input character c (in which case c is extracted).

Remarks: The last value will occur if traits::eq_type(delim, traits::eof()).

Returns: *this.

int_type peek();
Effects: Behaves as an unformatted input function (as described above). After constructing a sentry object, does not extract the current character.
Returns: traits::eof() if it is false. Otherwise, returns rdbuf()->get().

basic_istream<charT, traits>& read(charT* s, streamsize n);
Effects: Behaves as an unformatted input function (as described above). After constructing a sentry object, if good() calls setstate(failbit) which may throw an exception, and return. Otherwise extracts characters and stores them into successive locations of an array whose first element is defined by s. Characters are extracted until one of the following:

- (0.1) n characters are stored;
- (0.2) end-of-file occurs on the input sequence (in which case the function calls setstate(failbit | eof), which may throw ios_base::failure(30.5.5.4));

Returns: *this.

streamsize read(charT* s, streamsize n);
Effects: Behaves as an unformatted input function (as described above). After constructing a sentry object, if good() calls setstate(failbit) which may throw an exception, and return. Otherwise extracts characters and stores them into successive locations of an array whose first element is designated by s. If rdbuf()->in_avail() == -1, calls setstate(eof) (which may throw ios_base::failure(30.5.5.4)), and extracts no characters;

- (2.1) If rdbuf()->in_avail() == 0, extracts no characters
- (2.2) If rdbuf()->in_avail() > 0, extracts min(rdbuf()->in_avail(), n)).

Returns: The number of characters extracted.

basic_istream<charT, traits>& putback(charT c);
Effects: Behaves as an unformatted input function (as described above), except that the function clears EOF. After constructing a sentry object, if good() calls setstate(failbit) which may throw an exception, and return. If good(), rdbuf()->putback(c). If putback returns traits::badbit() (which may throw ios_base::failure(30.5.5.4)). Note: This extracts no characters, so the value returned by the next call to get() is 0.

Returns: *this.

basic_istream<charT, traits>& unset();
Effects: Behaves as an unformatted input function (as described above), except that the function is not overloaded over signed char and unsigned char.

Note that this function is not overloaded over signed char and unsigned char.

first clearssofbit. After constructing a sentry object, if !good() calls setState(failbit) which may throw an exception, and return. If rdbuf() is not null, rdbuf()->sunget(). If rdbuf() is null, or if getc() calls traits::eof(), setState(badbit) which may throw ios_base::failure(30.5.5.4). Note: This function extracts no characters, so the value returned by the next call to gcount() is 0.

Returns: *this.

int stync();
Effects: Behaves as an unformatted function (as described above), except that it does not count the number of characters extracted and does not affect the value returned by subsequent calls to gcount(). After constructing a sentry object, if rdbuf() is a null pointer, returns -1. Otherwise, rdbuf()->pubsync() and if returns -1 calls setState(badbit) (which may throw ios_base::failure(30.5.5.4)) and returns -1. Otherwise, returns zero.

pos_type tellsync();
Effects: Behaves as an unformatted function (as described above), except that it does not count the number of characters extracted and does not affect the value returned by subsequent calls to gcount().
Returns: After constructing a sentry object, if fail() != false, returns pos_type(-1) to indicate the position. Otherwise, returns rdbuf()->pubseekoff(0, cur, in).

basic_istream<traits&>&seekg(pos_type pos);
Effects: Behaves as an unformatted function (as described above), except that the function first clears eof, does not count the number of characters extracted, and does not affect the value returned by subsequent calls to gcount(). After constructing a sentry object, if fail() != true, returns rdbuf()->pubseekoff(off, dir, in). In case of failure, the function calls setState(badbit) (which may throw ios_base::failure).

Returns: *this.

basic_istream<traits&>&seekoff(off ios_base::seekdir);
Effects: Behaves as an unformatted function (as described above), except that the function first eof, does not count the number of characters extracted, and does not affect the value returned by subsequent calls to gcount(). After constructing a sentry object, if fail() != true, executes rdbuf()->pubseekoff(off, dir, in). In case of failure, the function calls setState(badbit) (which may throw ios_base::failure).

Returns: *this.

# 30.7.4 Standard basic_istream manipulators

[stream.manip]

template <class char, class traits>
basic_istreamchar<char, traits&>&ws();
Effects: Behaves as an unformatted function (30.7.4.3), except that it does not count the number of characters extracted and does not affect the value returned by subsequent calls to gcount(). After constructing a sentry object extracts characters as long as the next character c is whitespace or until there are no more characters in the sequence. Whitespace characters are distinguished with the same criterion as used by sentry::sentry(30.7.4.1.3). If ws stopping characters because there are no more available it sets eofbit, but not fail.

Returns: *is.
