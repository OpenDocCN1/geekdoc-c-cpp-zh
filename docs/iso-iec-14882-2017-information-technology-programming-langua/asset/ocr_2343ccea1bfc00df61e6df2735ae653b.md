# ISO/IEC 14882:2017(E)

use_facet<ctype<char>>(loc).is(ctype_base::F, c)

Where F is the type_base::mask value corresponding to function (25.4.1).232

# 25.3.3.2 Conversions

[conversions]

# 25.3.3.1 Character conversions

[conversions.character]

```
template<class charT> toupper(charT c, const locale& loc);
    return use_facet<ctype<charT>>(loc).toupper(c);
template<class charT> tolower(charT c, const locale& loc);
    return use_facet<ctype<charT>>(loc).tower(c);
```

# 25.4 Standard locale categories

+   1. Each of the standard classes includes a family of facets. Some of these implementing format or parsing of a data, by use or users' livestream operators << and >>, as members put() and get(), respectively. Each member function returns an io_base::argument flags(), precision(), and width(), the form of the formatting argument (30.5.3). Those functions which need to use other facets call its member getloc() to retrieve the locale imbued them. Formatting facets use the character argument to fill the specified width where necessary.
2. The put() members make no provision for error reporting. (Any failures of the OutputIterator argument can be extracted from the returned iterator.) The get() members make an io_base::istate argument whose value they ignore, be set to io_base::failbit in a parse error.
3. Within this class is expected that one virtual function calls another virtual function.

# 25.4.1 The type category

[category.type]

```
namespace std {
    class ctype_base {
    public:
        using mask = see;
        // numeric values are for hex option only.
        static const mask space = 1 << 0;
        static const mask print = 1 << 1;
        static const mask cntrl = 1 << 2;
        static const mask upper = 1 << 3;
        static const mask lower = 1 << 4;
        static const mask alpha = 1 << 5;
        static const mask digit = 1 << 6;
        static const mask punct = 1 << 7;
        static const mask zdigit = 1 << 8;
        static const mask blank = 1 << 9;
        static const mask alphanum = alphanum | digit;
        static const mask graph = alphanum | punct;
    };}
```

+   1. The type mask is a bitmask type (20.4.2.1.4).