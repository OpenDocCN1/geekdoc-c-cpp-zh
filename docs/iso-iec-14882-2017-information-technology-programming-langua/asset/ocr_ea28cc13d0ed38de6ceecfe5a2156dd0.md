# ISO/IEC 14882:2017(E)

# 25.4.6 The monetary category [category.monetary]

1 These templates handle monetary formats. A template parameter indicates whether local or international monetary formats are to be used.

2 All specifications of member functions for money_put and money_get in the subclasses of 25.4.6 only apply to the specializations required in Tables 69 and 70 (25.3.1.1.1). Their members use ios_base, ios_base::iotostate, and fill arguments as described in 25.4, and the moneypunt<> and ctype<> facets, to

# 25.4.6.1 Class money_get [locale.money.get]

```
namespace std {
template<charT, class InputIterator = istream_iterator<charT>>
class money_get : public locale::facet {
public:
    using char_type = charT;
    using iter_type = InputIterator;
    using string_type = basic_string<charT>;

    explicit money_get(size_t refs = 0);

    iter_type get(iter_type s, iter_type end, bool int,
                  ios_base& f, ios_base::iotostate& err,
                  long double units) const;
    iter_type get(iter_type s, iter_type end, bool int,
                  ios_base& f, ios_base::iotostate& err,
                  string_type digits) const;

    static locale_id id;

protected:
    money_get();
    virtual iter_type do_get(iter_type s, iter_type end, bool int, ios_base& f,
                             ios_base::iotostate& err, long double units) const;
    virtual iter_type do_get(iter_type s, iter_type end, bool int, ios_base& f,
                             ios_base::iotostate& err, string_type digits) const;

};

```

# 25.4.6.1 money_get members [locale.money.get.members]

```
iter_type get(iter_type s, iter_type end, bool int, ios_base& f, ios_base::iotostate& err, long double units) const;
iter_type get(iter_type s, iter_type end, bool int, ios_base& f, ios_base::iotostate& err, string_type digits) const;
```

1 Returns: do_get(s, end, int, f, quant).

# 25.4.6.2 money_get virtual functions [locale.money.virtual]

```
iter_type do_get(iter_type s, iter_type end, bool int, ios_base str, ios_base::iotostate& err, long double units) const;
iter_type do_get(iter_type s, iter_type end, bool int, ios_base str, ios_base::iotostate& err, string_type digits) const;
```

1 Effects: Reads characters from s to parse and construct a monetary value according to the format specified by a moneypunt<charT, Int> facet reference mp and the character mapping specified by a ctype<charT> facet obtained from the locale returned by str.getloc(s), and str.flags().

§ 25.4.6.1.2 ©/IEC 2017 - All rights reserved 815