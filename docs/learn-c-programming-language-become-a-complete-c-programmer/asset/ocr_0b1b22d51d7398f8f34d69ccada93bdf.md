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

# 39.4.1 string Comparison

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