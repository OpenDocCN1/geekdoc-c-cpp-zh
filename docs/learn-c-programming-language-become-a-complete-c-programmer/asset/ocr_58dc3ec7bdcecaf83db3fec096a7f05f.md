classes marked with <> are templates parameterized by a character type and containing a locale. The I/O stream operations:

+   - Are type-safe and type sensitive
+   - Are extensible (when someone designs a new type, matching I/O stream operators can be added without modifying existing code)

# Section 38.1 Introduction 1075

+   - Are locale sensitive (Chapter 39)
+   - Are efficient (though their potential is not always fully realized)
+   - Are interoperable with C-style stdio (§43.3)
+   - Include formatted, unformatted, and character-level operations

The basic_iostream is defined based on basic_istream (§38.6.2) and basic_ostream (§38.6.1):

```
template<typename C, typename Tr = char_traits<C>>
class basic_iostream :
public basic_istream<C,Tr>, public basic_ostream<C,Tr> {
public:
using char_type = C;
using int_type = typename Tr::int_type;
using pos_type = typename Tr::pos_type;
using off_type = typename Tr::off_type;
using traits_type = Tr;

explicit basic_iostream(basic_streambuf<C,Tr>* sb); virtual ~basic_iostream();
protected:
basic_iostream(const basic_iostream& rhs) = delete;
basic_iostream(basic_iostream&& rhs);

basic_iostream& operator=(const basic_iostream& rhs) = delete;
basic_iostream& operator=(basic_iostream&& rhs);
void swap(basic_iostream& rhs);
};
```

The template parameters specify the character type and the traits used to manipulate characters (§36.2.2), respectively.

Note that no copy operations are provided: sharing or cloning the fairly complex state of a stream would be difficult to implement and expensive to use. The move operations are intended for use by derived classes and are therefore protected. Moving an iostream without moving the state of its defining derived class (e.g., an fstream) would lead to errors.

There are three standard streams:

# Standard I/O Streams

cout The standard character output (often by default a screen) cin The standard character input (often by default a keyboard) cerr The standard character error output (unbuffered) clog The standard character error output (buffered)