
```
"winter"
};
```

Then, we override the Season_io functions that convert between the string representation and the enumerators:

```
const string& US_season_io::to_str(Season x) const
{
if (x<spring || winter<x) {
static const string ss = "no-such-season"; return ss;
}
return seasons[x];
}
bool US_season_io::from_str(const string& s, Season& x) const {
const string*p= find(begin(seasons),end(seasons),s); if (p==end)
return false;
x = Season(p-begin(seasons));
return true;
}
```

Note that because US_season_io is simply an implementation of the Season_io interface, I did not define an id for US_season_io. In fact, if we want US_season_io to be used as a Season_io, we must not give US_season_io its own id. Operations on locales, such as has_facet (§39.3.1), rely on facets implementing the same concepts being identified by the same id (§39.3).

The only interesting implementation question is what to do if asked to output an invalid Season. Naturally, that shouldn’t happen. However, it is not uncommon to find an invalid value for a simple user-defined type, so it is realistic to take that possibility into account. I could have thrown an exception, but when dealing with simple output intended for humans to read, it is often helpful to produce an “out-of-range” representation for an out-of-range value. Note that for input, the errorhandling policy is left to the >> operator, whereas for output, the facet function to_str() implements an error-handling policy. This was done to illustrate the design alternatives. In a “production design,” the facet functions would either implement error handling for both input and output or just report errors for >> and << to handle.

This Season_io design relies on derived classes to supply the locale-specific strings. An alternative design would have Season_io itself retrieve those strings from a locale-specific repository (see §39.4.7). The possibility of having a single Season_io class to which the season strings are passed as constructor arguments is left as an exercise.

## 39.3.3 Uses of locales and facets

The primary use of locales within the standard library is in I/O streams. However, the locale mechanism is a general and extensible mechanism for representing culture-sensitive information. The messages facet (§39.4.7) is an example of a facet that has nothing to do

with I/O streams. Extensions to the iostream library and even I/O facilities that are not based on streams might take advantage of locales. Also, a user may use locale as a convenient way of organizing arbitrary culturesensitive information.

Because of the generality of the locale/facet mechanism, the possibilities for user-defined facets are unlimited. Plausible candidates for representation as facets are dates, time zones, phone numbers, social security numbers (personal identification numbers), product codes, temperatures, general (unit,value) pairs, postal codes (zip codes), clothing sizes, and ISBN numbers.

As with every other powerful mechanism, facets should be used with care. That something can be represented as a facet doesn’t mean that it is best represented that way. The key issues to consider when selecting a representation for cultural dependencies are – as ever – how the various decisions affect the difficulty of writing code, the ease of reading the resulting code, the maintainability of the resulting program, and the efficiency in time and space of the resulting I/O operations.

## 39.4 Standard facets

In <locale>, the standard library provides these facets: Standard facets (§iso.22.3.1.1.1)

collate numeric
String comparison Numeric formatting

monetary Money formatting

time Date and time formatting

ctype Character classification

messages Message retrieval

collate<C> §39.4.1

numpunct<C> §39.4.2

num_get<C,In>

num_put<C,Out>

moneypunct<C> §39.4.3

moneypunct<C,International>

money_get<C,In>

money_put<C,Out>

time_put<C,Out> §39.4.4

time_put_byname<C,Out>

time_get<C,In>

ctype<C> §39.4.5

codecvt<In,Ex,SS>

codecvt_byname<In,Ex,SS>

messages<C> §39.4.7

The details are explained in the referenced subsections.

When instantiating a facet from this table, C must be a character type (§36.1). These facets are guaranteed to be defined for char or wchar_t. In addition, ctype<C> is guaranteed to support char16_t and char32_t. A user who needs standard I/O to deal with another character type X must rely on implementation-specific facet specializations or provide suitable versions of facets for X. For example, codecvt<X,char,mbstate_t>

(§39.4.6) might be needed to control conversions between X and char.
International can be true or false; true means that a three-character (plus zero terminator) “international” representation of a currency symbol is used (§39.4.3.1), such as USD and BRL. A shift-state parameter, SS, is used to represent the shift states of a multibyte character representation (§39.4.6). In <cwchar>, mbstate_t is defined to represent any of the conversion states that can occur in an implementation-defined set of supported multibyte character encoding rules. The equivalent to mbstate_t for an arbitrary character type X is char_traits<X>::state_type (§36.2.2). In and Out are input iterators and output iterators, respectively (§33.1.2, §33.1.4). Providing the _put and _get facets with these template arguments allows a programmer to provide facets that access nonstandard buffers (§39.4.2.2). Buffers associated with iostreams are stream buffers, so the iterators provided for those are ostreambuf_iterator s (§38.6.3, §39.4.2.2). Consequently, the function failed() is available for error handling (§38.6.3).
Each standard facet has a _byname version. An F_byname facet is derived from the facet F.
F_byname provides the identical interface to F, except that it adds a constructor taking a string argument naming a locale (e.g., see §39.4.1). The F_byname(name) provides the appropriate semantics for F defined in locale(name). For example:
Section 39.4 Standard facets 1125
sort(v.begin(),v.end(),collate_byname{"da_DK"}); // sorting using character comparison from “da_DK” The idea is to pick a version of a standard facet from a named locale (§39.2.1) in the program’s execution environment. This implies that _byname constructors are very slow compared to constructors that do not need to consult the environment. It is almost always faster to construct a locale and then to access its facets than it is to use _byname facets in many places in a program. Thus, reading a facet from the environment once and then using the copy in main memory repeatedly is usually a good idea. For example:
locale dk {"da_DK"}; // read the Danish locale (including all of its facets) once
// then use the dk locale and its facets as needed
void f(vector<string>& v, const locale& loc) {
const collate<char>& col {use_facet<collate<char>>(dk)}; const ctype<char>& ctyp {use_facet<ctype<char>>(dk)};
locale dk1 {loc,&col}; locale dk2 {dk1,&ctyp};
// use Danish string comparison
// use Danish character classification and string comparison
sort(v.begin(),v.end(),dk2);

```
// ...
}
```

This dk2 locale will use Danish-style strings but will retain the default conventions for numbers.

The notion of categories gives a simpler way of manipulating standard facet in locales. For example, given the dk locale, we can construct a locale that reads and compares strings according to the rules of Danish (which has three more vowels than English) but that retains the syntax of numbers used in C++:

```
locale dk_us(locale::classic(),dk,collate|ctype); // Danish letters,Americannumbers
```

The presentations of individual standard facet contain more examples of facet use. In particular, the discussion of collate (§39.4.1) brings out many of the common structural aspects of facets.

Standard facets often depend on each other. For example, num_put depends on numpunct. Only if you have a detailed knowledge of individual facets can you successfully mix and match facets or add new versions of the standard facets. In other words, beyond the simple operations (such as imbue() for iostreams and using collate for sort()), the locale mechanisms are not meant to be directly used by novices. For an extensive discussion of locales, see [Langer,2000].

The design of an individual facet is often messy. The reason is partially that facets have to reflect messy cultural conventions outside the control of the library designer, and partially that the C++ standard library-facilities have to remain largely compatible with what is offered by the C standard library and various platform-specific standards.

On the other hand, the framework provided by locales and facet is general and flexible. A facet can be designed to hold any data, and the facet’s operations can provide any desired operation based on that data. If the behavior of a new facet isn’t overconstrained by convention, its design can be simple and clean (§39.3.2).

### 39.4.1 string Comparison

The standard collate facet provides ways of comparing arrays of characters:

```
template<class C>
class collate : public locale::facet {
public:
using char_type = C;
using string_type = basic_string<C>;
explicit collate(size_t = 0);
int compare(const C* b, const C* e, const C* b2, const C* e2) const { return do_compare(b,e,b2,e2); }
long hash(const C * b, const C* e) const
{ return do_hash(b,e); }
string_type transform(const C* b, const C* e) const { return do_transform(b,e); }
static locale::id id; // facet identifier object (§39.2, §39.3, §39.3.1)
```
