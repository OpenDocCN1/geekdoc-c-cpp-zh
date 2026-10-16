
implementation character set to determine collation order (§32.6, §31.2.2.1).

## 39.3 Class facet

A locale is a collection of facets. A facet represents one specific cultural aspect, such as how a number is represented on output (num_put), how a date is read from input (time_get), and how characters are stored in a file (codecvt). The standard-library facets are listed in §39.4.

A user can define new facets, such as a facet determining how the names of the seasons are printed (§39.3.2).

A facet is represented in a program as an object of a class derived from std::locale::facet. Like all other locale facilities, facet is found in <locale>:

Section 39.3 Class facet 1119

```
class locale::facet {
protected:
explicit facet(size_t refs = 0);
virtual ~facet();
facet(const facet&) = delete;
void operator=(const facet&) = delete;
};
```

The facet class is designed to be a base class and has no public functions. Its constructor is protected to prevent the creation of “plain facet” objects, and its destructor is virtual to ensure proper destruction of derived-class objects.

A facet is intended to be managed through pointers stored in locales. A 0 argument to the facet constructor means that locale should delete the facet when the last reference to it goes away. Conversely, a nonzero constructor argument ensures that locale never deletes the facet. A nonzero argument is meant for the rare case in which the lifetime of a facet is controlled directly by the programmer rather than indirectly through a locale.

Each kind of facet interface must have a separate id:

```
class locale::id {
public:
id();
void operator=(const id&) = delete;
id(const id&) = delete;
};
```

The intended use of id is for the user to define a static member of type id of each class supplying a new facet interface (for example, see §39.4.1). The locale mechanisms use ids to identify facets (§39.2, §39.3.1). In the obvious implementation of a locale, an id is used as an index into a vector of pointers to facets, thereby implementing an efficient map<id,facet*>.

Data used to define a (derived) facet is defined in the derived class. This implies that the programmer defining a facet has full control over the data and that arbitrary amounts of
data can be used to implement the concept represented by a facet.

A facet is intended to be immutable, so all member functions of a user-defined facet should be defined const.

### 39.3.1 Accessing facets in a locale

The facets of a locale are accessed using two template functions:

Non-member locale functions ( [siso.22.3.2](#) )

`f=use_facet<F>(loc)` is a reference to the facet F in loc; throw bad_cast if loc doesn’t have F

`has_facet<F>(loc)` Does loc have facet F? noexcept

Think of these functions as doing a lookup in their locale argument for their template parameter F. Alternatively, think of use_facet as a kind of explicit type conversion (cast) of a locale to a specific facet. This is feasible because a locale can have only one facet of a given type. For example:

```
void f(const locale& my_locale) {
  char c = use_facet<numpunct<char>>(my_locale).decimal_point() // use standard facet // …

  if (has_facet<Encrypt>(my_locale)) { // does my_locale contain an Encrypt facet? const Encrypt& f = use_facet<Encrypt>(my_locale); const Crypto c = f.get_crypto();
    // …
  }
  // …
}
// retrieveEncryptfacet // use Encrypt facet
```

The standard facets are guaranteed to be available for all locales (§39.4), so we don’t need to use has_facet for standard facets.

One way of looking at the facet::id mechanism is as an optimized implementation of a form of compile-time polymorphism. A dynamic_cast can be used to get very similar results to what use_facet produces. However, the specialized use_facet can be implemented more efficiently than the general dynamic_cast.

An id identifies an interface and a behavior rather than a class. That is, if two facet classes have exactly the same interface and implement the same semantics (as far as a locale is concerned), they should be identified by the same id. For example, collate<char> and collate_byname<char> are interchangeable in a locale, so both are identified by collate<char>::id (§39.4.1).

If we define a facet with a new interface – such as Encrypt in f() – we must define a corresponding id to identify it (see §39.3.2 and §39.4.1).

### 39.3.2 A Simple User-Defined facet

The standard library provides standard facets for the most critical areas of cultural
differences, such as character sets and I/O of numbers. To examine the facet mechanism in isolation from the complexities of widely used types and the efficiency concerns that accompany them, let me first present a facet for a trivial user-defined type:

```
enum Season { spring, summer, fall, winter }; // verysimple user-defined type
```

The style of I/O outlined here can be used with little variation for most simple user-defined types.

```
class Season_io : public locale::facet {
public:
Season_io(int i = 0) : locale::facet{i} { }
~Season_io() { } // to makeitpossible to destroySeason_io objects (§39.3)
virtual const string& to_str(Season x) const = 0; // stringrepresentation of x
virtual bool from_str(const string& s, Season& x) const = 0; // place Season for s in x
static locale::id id; // facet identifier object (§39.2, §39.3, §39.3.1) };
locale::id Season_io::id; // define the identifier object
```

For simplicity, this facet is limited to strings of chars.

The Season_io class provides a general and abstract interface for all Season_io facets. To define the I/O representation of a Season for a particular locale, we derive a class from Season_io, defining to_str() and from_str() appropriately.

Output of a Season is easy. If the stream has a Season_io facet, we can use that to convert the value into a string. If not, we can output the int value of the Season:

```
ostream& operator<<(ostream& os, Season x)
{
locale loc {os.getloc()}; // extract the stream’slocale (§38.4.4)
if (has_facet<Season_io>(loc))
return os << use_facet<Season_io>(loc).to_str(x); // stringrepresentation
return os << static_cast<int>(x); // integer representation }
```

For maximum efficiency and flexibility, standard facets tend to operate directly on stream buffers (§39.4.2.2, §39.4.2.3). However, for a simple user-defined type, such as Season, there is no need to drop to the streambuf level of abstraction.

As is typical, input is a bit more complicated than output:

```
istream& operator>>(istream& is, Season& x)
{
const locale& loc {is.getloc()}; // extract the stream’slocale (§38.4.4)
if (has_facet<Season_io>(loc)) {
const Season_io& f {use_facet<Season_io>(loc)}; // get hold of the locale’sSeason_io facet
string buf;
if (!(is>>buf && f.from_str(buf,x))) is.setstate(ios_base::failbit); return is;
}
// read alphabetic representation
```

```
int i;
is >> i;
x = static_cast<Season>(i); return is;
}
```

```
// read numeric representation
```

The error handling is simple and follows the error-handling style for built-in types. That is, if the input string didn’t represent a Season in the chosen locale, the stream is put into the fail state. If exceptions are enabled, this implies that an ios_base::failure exception is thrown (§38.3).

Here is a trivial test program:

```
int main()
// a trivial test
{
Season x;

// use the default locale (no Season_io facet) implies integer I/O: cin >> x;
cout << x << endl;

locale loc(locale(),new US_season_io{});
cout.imbue(loc); // use locale with Season_io facet cin.imbue(loc); // use locale with Season_io facet

cin >> x;
cout << x << endl;
}
```

Given the input

```
2
```

```
summer
```

this program responds:

```
2
```

```
summer
```

To get this, we must derive a class US_season_io from Season_io, and define an appropriate string representation of the seasons:

```
class US_season_io : public Season_io {
static const string seasons[];
public:
const string& to_str(Season) const;
bool from_str(const string&, Season&) const;

// note: no US_season_io::id };
```

```
const string US_season_io::seasons[] = {
"spring",
"summer",
"fall",
