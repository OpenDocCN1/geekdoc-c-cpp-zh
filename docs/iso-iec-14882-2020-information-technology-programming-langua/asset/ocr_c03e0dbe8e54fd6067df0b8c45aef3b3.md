# ISO/IEC 14882:2020(E)

5 For some standard facets a standard "..._byname" class, derived from it, implements the virtual function semantics equivalent to that facet of the locale constructed by locale(const char*) with the same name. Each such facet provides a constructor that takes a const char* argument, which names the locale, and a refs argument, which is passed to the base class constructor. Each such facet also provides a constructor that takes a string argument str and a refs argument, which has the same effect as calling the first constructor with the two arguments str.c_str() and refs. If there is no "..._byname" version of a facet, the base class implements named locale semantics itself by reference to other facets.

# 28.3.1.2.3 Class locale::id [locale.id]

```
namespace std {
  class locale::id {
  public:
    id();
    void operator=(const id&) = delete;
    id(const id&) = delete;
  };
}
```

1 The class locale::id provides identification of a locale facet interface, used as an index for lookup and to encapsulate initialization.

> 2 [Note 1: Because facets are used by iostreams, potentially while static constructors are running, their initialization cannot depend on programmed static initialization. One initialization strategy is for locale to initialize each facet's id member the first time an instance of the facet is installed into a locale. This depends only on static storage being zero before constructors run (6.9.3.2). — end note]

# 28.3.1.3 Constructors and destructor [locale.cons]

```
locale() noexcept;
```

1 Effects: Constructs a copy of the argument last passed to locale::global(locale&), if it has been called; else, the resulting facets have virtual function semantics identical to those of locale::classic().

> [Note 1: This constructor yields a copy of the current global locale. It is commonly used as a default argument for function parameters of type const locale&. — end note]

```
explicit locale(const char* std_name);
```

2 Effects: Constructs a locale using standard C locale names, e.g., "POSIX". The resulting locale implements semantics defined to be associated with that name.

3 Throws: runtime_error if the argument is not valid, or is null.

4 Remarks: The set of valid string argument values is "C", "", and any implementation-defined values.

```
explicit locale(const string& std_name);
```

5 Effects: The same as locale(std_name.c_str()).

```
locale(const locale& other, const char* std_name, category);
```

6 Effects: Constructs a locale as a copy of other except for the facets identified by the category argument, which instead implement the same semantics as locale(std_name).

7 Throws: runtime_error if the argument is not valid, or is null.

8 Remarks: The locale has a name if and only if other has a name.

```
locale(const locale& other, const string& std_name, category cat);
```

9 Effects: The same as locale(other, std_name.c_str(), cat).

```
template<class Facet> locale(const locale& other, Facet* f);
```

10 Effects: Constructs a locale incorporating all facets from the first argument except that of type Facet, and installs the second argument as the remaining facet. If f is null, the resulting object is a copy of other.

11 Remarks: The resulting locale has no name.