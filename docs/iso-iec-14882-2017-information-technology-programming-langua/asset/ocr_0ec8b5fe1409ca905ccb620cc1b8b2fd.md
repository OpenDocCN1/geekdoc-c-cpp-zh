# ISO/IEC 14882:2017(E)

# 30.5.6.4 floatfield manipulators

ios_base fixed(ios_base str);

+   1 Effects: Calls str.setf(ios_base::fixed, ios_base::floatfield).
2 Returns: str.

ios_base scientific(ios_base str);

+   3 Effects: Calls str.setf(ios_base::scientific, ios_base::floatfield).
4 Returns: str.

ios_base hexfloat(ios_base str);

+   5 Effects: Calls str.setf(ios_base::fixed | ios_base::scientific, ios_base::floatfield).
6 Returns: str.

> > Note: The most obvious use of ios_base::hex for hexadecimal floating-point format would change the meaning of using well-defined programs. C++ 2003 gives no meaning to the combination of fixed and scientific. — end note

ios_base defaultfloat(ios_base str);

+   8 Effects: Calls str.unsetf(ios_base::floatfield).
9 Returns: str.

# 30.5.6.5 Error reporting [error.reporting]

error_code make_error_code(io_err eoe) noexcept;

+   1 Returns: error_code(static_cast<int>(eoe), iostream_category()).
2 error_condition_make_error_condition(io_err eoe) noexcept;
3 Returns: error_condition(static_cast<int>(eoe), iostream_category()).

const error_category& iostream_category() noexcept;

+   4 Returns: A reference to an object of type derived from class error_category.
The object's default_error_condition and equivalent virtual functions shall behave as specified for the class error_category. The object's name virtual function shall return a pointer to the string "iostream".

# 30.6 Stream buffers [stream.buffers]

# 30.6.1 Header <streambuf> synopsis [stream.buffers.syn]

```
namespace std {
    template <class char, class traits = char_traits<char>>
class basic_streambuf {
        using streambuf = basic_streambuf<char>;n        using wstreambuf = basic_streambuf<char, traits>;
    }
```

+   1 The header <streambuf> defines types that control input from and output to character sequences.
1 Stream buffers can impose various constraints on the sequences they control. Some constraints are:

# 30.6.2 Stream buffer requirements [streambuf.reqts]

+   (1.1) The controlled input sequence can not be readable.

§ 30.6.2 ©ISO/IEC 2017 – All rights reserved 1175