# ISO/IEC 14882:2017(E)

# 30.6.3.4.5 Put area

streamize xput(const char_type*, streamize n);

+   1 Effects: Writes xput to n characters to the output sequence if repeated calls to sput(c). The characters written are obtained from successive elements of the array whose first element is designated by s. Writing opts either when n characters have been written or a call to sput(c) would return traits::eof(). It is unspecified whether function overflow() occurs when pptr() == epptr() becomes true or whether it achieves the same effect by other means.

+   2 Returns: The number of characters written.

```
int_type overflow(int_type c = traits::eof());
```

+   3 Effects: Consumes some initial subsequence of the characters of the pending sequence. The pending sequence is defined as the concatenation of

+   (3.1) the empty sequence if pbase() is null, otherwise pptr() - pbase() characters starting at pbase(), followed by pptr() - pbase().

+   (3.2) the empty sequence if eq_int_type(c, traits::eof()) returns true, otherwise the sequence consisting of

+   4 Remarks: The member functions sput() and sput() call this function in case that no room can be in the put buffer to accommodate the argument sequence.

+   5 Requires: Every overdefining of a character on the associated output sequence is specified 303

+   1 Let r be the number of characters consumed from the pending sequence. If r is not considered in base pbase() and pptr() call then so that: pptr() - pbase() == r and the characters starting at pbase() are the associated output. If r is zero (all characters of the pending sequence have been consumed) then pbase() is set to null, or pbase() and pptr() are set to the same null value.

+   3 The function may fail if either adding some character to the associated output stream fails or if it is unable to establish pbase() and pptr() according to the rules.

+   6 Returns: traits::eof() or throws an exception if the function fails.

Otherwise, returns some value other than traits::eof(). 304

Default behavior: Returns traits::eof().

# 30.7 Formatting and manipulators

# 30.7.1 Header <iostream> synopsis

```
namespace std {
    template <class char, class traits = char_traits<char>>
    basic_istream;
```

```
using istream = basic_istream<char>;
using widest = basic_istream<char_t>;
```

```
template <class char, class traits = char_traits<char>>
    basic_iostream;
```

303 That is, for each class derived from an instance of basic_streambuf in Clause (30.8.2, 30.9.2), a specification of how consuming a character affects the associated output sequence is given. There is no requirement on a program-defined class.

304 Typically, overflow returns c to indicate success, except when traits::eq_int_type(c, traits::eof()) returns true, in which case it returns traits::not_eof(c).