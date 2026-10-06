# ISO/IEC 14882:2017(E)

```
typename basic_ostream<charT, traits>::sentry cerberos(s);
if (cerberos) {
    ios_base::ostate err = ios_base::ostate::goodbit;
    tm tbuf = extract(tbuf);
    time_t(time_iterator<charT, ostreambuf_iterator<charT>> >(
        s.getfile()).put(s, s.fill(), &tbuf, 'r');
    ) s.setstate(err); // might throw

    return s;
}
```

+   - end example
- In the call to use_facet<Facet>(loc), the type argument chooses a facet, making available members of the named type. If facet is not present in a locale, it throws the standard exception bad_cast. A C++ program can check if a locale implements a particular function with the type has_facet<Facet>(). User-defined facets may be installed in a locale, and used identically as to the standard collections (25.4.8).

+   - [Note: A member template operator()(const basic_string<C, T, A>&, const basic_string<C, T, A>) is provided so that a locale may be used as a predicate argument to collate strings.

+   - Convenient global interfaces are provided for traditional facet functions such as isdigit() and isspace(), so that a generic locale object a C++ program can call isspace(c, loc). This cases upon upgrading existing constructors (30.7.4.2).

+   - Once a reference is obtained from a locale by calling use_facet, reference remains valid, and the results from functions of it can be cached and re-used, as long as locale reference refers to that facet.

+   - In successive calls to a locale facet member on a facet object in the same locale, the returned result should be identical.

+   - A locale is constructed from a string "*", from parts of two named locales, it has a name; all others do not. Named locales may be compared for equality; an unnamed locale is equal only to (copies of) itself. For an unnamed locale, locale::name() returns the string "*

+   - Whether there is one global object or one global object per thread is implementation-defined. Implementations should provide one global object per thread. If there is a single global object for the entire program, implementations are not required to avoid data races on it (20.5.5.9).

25.5.1.1 locale types

25.5.1.1.1 Type::category; [locale.category]

Valid values include the locale facet bitmask collate, ctype, monetary, numeric, time, and messages, each which represents a single category. In addition, locale bitmask constant none is defined as zero and represents no category. Locale bitmask constant all is defined such that the expression

```
(collate | ctype | monetary | time | messages | all) == all is true, and the union of all categories. Further, the expression (X | Y), where X and Y represent a single category, represents the union of the two categories.
```