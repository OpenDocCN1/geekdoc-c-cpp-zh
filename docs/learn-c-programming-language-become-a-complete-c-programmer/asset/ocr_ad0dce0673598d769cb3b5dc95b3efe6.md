(e.g., by a cin.setstate(ios_base::badbit)):
cin.exceptions(cin.exceptions()|ios_base::badbit);
For example:

```
struct Io_guard { // RAII class for iostream exceptions
iostream& s;
auto old_e = s.exceptions();
Io_guard(iostream& ss, ios_base::iostate e) :s{ss} { s.exceptions(s.exceptions()|e); }
~Io_guard() { s.exceptions(old_e); }
```

# Section 38.3 Error Handling 1081

```
void use(istream& is) {
Io_guard guard(is.ios_base::badbit);
// ... use is ...
}
catch (ios_base::badbit) {
// ... bail out! ...
}
```

I tend to use exceptions to handle iostream errors that I don’t expect to be able to recover from. That usually means all bad() exceptions.

# 38.4 I/O Operations

The complexity of the I/O operations reflects tradition, the need for I/O performance, and the variety of human expectations. The description here is based on the conventional English small character set (ASCII). The ways in which different character sets and different natural languages are handled are described in Chapter 39.

# 38.4.1 Input Operations

Input operations are provided by istream (§38.6.2), found in <istream> except for the ones reading into a string; those are found in <string>. The basic_istream is primarily intended as a base class for more specific input classes, such as istream and istringstream:

```
template<typename C, typename Tr = char_traits<C>>
class basic_istream : virtual public basic_ios<C,Tr> {
public:
using char_type = C;
using int_type = typename Tr::int_type;
using pos_type = typename Tr::pos_type;
using off_type = typename Tr::off_type;
using traits_type = Tr;
explicit basic_istream(basic_streambuf<C,Tr>* sb); virtual ~basic_istream(); // release all resources
class sentry;
```