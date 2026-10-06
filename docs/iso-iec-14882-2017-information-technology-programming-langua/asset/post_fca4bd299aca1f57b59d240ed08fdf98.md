
# ISO/IEC 14882:2017(E)

locale member functions expecting a category one of the categories defined above, or the union of two or more such values. Such a category value identifies a set of locale categories. Each locale category, in turn, identifies a set of locale facets, including at least those in Table 69.

Table 69 — Locale category facets

| Category | Includes facets |
| --- | --- |
| collate | collate<char>, collate<wchar_t> |
| ctype | ctype<char>, ctype<wchar_t>, codecvt<char>, codecvt<wchar_t>, codecvt<char16_t>, codecvt<mbstate_t>, codecvt<char32_t>, codecvt<mbstate_t>, codecvt<wchar_t>, codecvt<mbstate_t> |
| monetary | moneyput<char>, moneyput<wchar_t>, moneyput<char, true>, moneyput<wchar_t, true>, money_get<char>, money_get<wchar_t>, money_put<char>, money_put<wchar_t> |
| numeric | numput<char>, numput<wchar_t>, num_get<char>, num_get<wchar_t>, num_put<char>, num_put<wchar_t> |
| time | time_get<char>, time_get<wchar_t>, time_put<char>, time_put<wchar_t> |
| messages | messages<char>, messages<wchar_t> |

3 For any locale constructed, or from locale::classid(), and any facet shown in Table 69, has_facet>() is true. Each locale member function which takes a locale::category argument operates on the corresponding set of facets.

4 An implementation is required to provide those specializations for facet templates identified as members of a category, and for those shown in Table 70.

5 The provided implementation of members name num_get<char> and num_put<char> use_facet<F>() only for F of types num_get<char> and ctype<char>, and for locale the value obtained by calling member get(ios_base*)

6 In declarations of members, a template name InputIterator or OutputIterator indicates the set of possible specializations on parameters that satisfy the requirements of InputIterator or OutputIterator. A template with name C represents the set of types that satisfies the requirements for char, wchar_t, and any other implementation-defined types on which any of iostream components can be instantiated. A template with name boolean represents the set of all specializations.

## 25.3.1.1.2 Locale::facet

```cpp
namespace std {
  class locale::facet {
  protected:
    explicit facet(size_t refs = 0);
    virtual ~facet();
    facet(const facet&) = delete;
    void operator=(const facet&) = delete;
  };
}
```

# ISO/IEC 14882:2017(E)

Table 70 — Required specializations

| Category | Includes facets |
| --- | --- |
| collate | collate_byname<char>, collate_byname<wchar_t> |
| ctype | ctype_byname<char>, ctype_byname<wchar_t> |
| codecvt | codecvt_byname<char, char, mbstate_t>, codecvt_byname<char_t, char, mbstate_t>, codecvt_byname<char32_t, char, mbstate_t>, codecvt_byname<wchar_t, char, mbstate_t> |
| monetary | money_byname<char>, money_byname<wchar_t> |
| numeric | num_byname<char>, num_byname<wchar_t> |
| time | time_byname<char>, time_byname<wchar_t> |
| put | put_char, put_time<char>, put<wchar_t>, put_byname<wchar_t> |
| messages | messages_byname<char>, messages_byname<wchar_t> |

1. Class facet is the base for locale facet sets. A facet is it if it is derived from another facet, or if it is a class derived from locale::facet and provides a publicly accessible declaration as follows: `static std::locale::id id;`

2. Template parameters in this Clause require them to be named Facet in declarations. A program that passes a type that is not a facet, or a type that refers to a volatile-qualified facet as an (explicit or deduced) argument to a locale function executing, is ill-formed. A const-qualified facet is a valid template argument to a locale function that executes a Facet template parameter.

3. The ref argument to the constructor is used for lifetime management. If refs == 0, the implementation deletes static_cast<facet*>(f) (where f is a pointer to the facet) when the last locale object containing the facet is destroyed; for refs == 1, the implementation never destroys the facet.

4. Constructors of all facets defined in this Clause take an argument and pass it to their facet base constructor. All one-argument constructors defined in this Clause are explicit, preventing their use in automatic conversions.

5. For some facet defined by a standard—byname", derived from it, the virtual function semantics equivalent to that of a locale constructed by locale(const char*) with the same name. Each facet provides a constructor that takes a const char argument, which names the locale, and a refs argument, which is passed to the facet base class. Each such facet also provides a constructor that takes a string argument and a refs argument, which has the same effect as calling the first constructor with the two arguments str.c_str() and refs. If there is no "...byname" version of the facet, the base class implements named semantics itself by reference to other facets.

## 25.3.1.1.3 Class locale::id

```cpp
namespace std {
    class locale::id {
    public:
        id();
        void operator=(const id& dk) = delete;
        id(const id& dk) = delete;
    };
}
```

The class locale::id provides identification of a locale facet interface, used as an index for lookup and initialization. Because facets are used by istreams, potentially while static constructors are running, their initialization cannot depend on static initialization. One initialization strategy is for locale to initialize each facet's id the first time an instance of the facet is installed into a locale.

## 25.3.1.2 locale constructors and destructor

locale() noexcept;
Default constructor: a snapshot of the current global locale. Effects: Constructs a copy of the last locale passed to locale::global(locale&), if it has been called; else, the results have virtual functions identical to that of locale::classic(). [Note: This is commonly used as the default value for all facets of functions that take a const locale& argument.]

locale(const locale other) noexcept;
Effects: Constructs a locale which is a copy of other.

```cpp
explicit locale(const char* std_name);
```
Constructs a locale using standard locale names, e.g., "POSIX". The resulting locale implements semantics defined to be associated with that name. Throws: runtime_error if the argument is not valid, or null. Remarks: The set of string argument values is "C", and any implementation-defined values.

```cpp
explicit locale(const string& std_name.c_str());
```

locale(const locale other, const char* std_name, category);
Constructs a locale as a copy of other except the facets by the category argument, which must implement the same semantics as locale(std_name). Throws: runtime_error if the argument is not valid, or null. Remarks: The locale has a name and only if it has a name.

```cpp
locale(const locale other, const string& std_name, category cat);
```
The same as locale(other, other std_name.c_str(), cat).

```cpp
template <class Facet> locale(const locale& other, Facet* f);
```
Constructs a locale incorporating all facets from the first argument except that of type Facet.
