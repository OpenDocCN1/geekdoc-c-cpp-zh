
The ios_base argument (here, cout) provides information about formatting state and locale. For example:

```
void test(ios_base& io) {
    locale loc = io.getloc();

    wchar_t wc = use_facet<ctype<char>>(loc).widen(c); // char to C conversion
    string s = use_facet<numpunct<char>>(loc).decimal_point(); // default: '.'
    string false_name = use_facet<numpunct<char>>(loc).falsename(); // default: "false"
}
```

A standard facet, such as num_put<char>, is typically used implicitly through a standard I/O stream function. Consequently, most programmers need not know about it. However, the use of such facets by standard-library functions is interesting because they show how I/O streams work and how facets can be used. As ever, the standard library provides examples of interesting programming techniques.

Using num_put, the implementer of ostream might write:

```
template<class C, class Tr>
basic_ostream<C,Tr>& basic_ostream<C,Tr>::operator<<(double d)
{
    sentry guard(*this); // see §38.4.1
    if (!guard) return *this;
    try {
        if (use_facet<num_put<C,Tr>>(getloc()).put(*this,*this,this->fill(),d).failed())
            setstate(badbit);
    }
    catch (...) {
        handle_ioexception(*this);
    }
    return *this;
}
```

A lot is going on here. The sentry ensures that all prefix and suffix operations are performed (§38.4.1). We get the ostream’s locale by calling its member function getloc() (§38.4.5.1). We extract num_put from that locale using use_facet (§39.3.1). That done, we call the appropriate put() function to do the real work. An ostreambuf_iterator can be constructed from an ostream (§38.6.3), and an ostream can be implicitly converted to its base class ios_base (§38.4.4), so the first two arguments to put() are easily supplied.

A call of put() returns its output iterator argument. This output iterator is obtained from a basic_ostream, so it is an ostreambuf_iterator. Consequently, failed() (§38.6.3) is available to test for failure and to allow us to set the stream state appropriately.

I did not use has_facet, because the standard facets (§39.4) are guaranteed to be present in every locale. If that guarantee is violated, bad_cast is thrown (§39.3.1). The put() function calls the virtual do_put(). Consequently, user-defined code may be executed, and operator<<() must be prepared to handle an exception thrown by the overriding do_put(). Also, num_put may not exist for some character types, so use_facet() might throw bad_cast (§39.3.1).

The behavior of a << for a built-in type, such as double, is defined by the C++ standard. Consequently, the question is not what handle_ioexception() should do but rather how it should do what the standard prescribes. If badbit is set in this ostream’s exception state (§38.3), the exception is simply re-thrown. Otherwise, an exception is handled by setting the stream state and continuing. In either case, badbit must be set in the stream state (§38.4.5.1):

```
template<class C, class Tr>
void handle_ioexception(basic_ostream<C,Tr>& s) // called from catch-clause
{
    if (s.exceptions()&ios_base::badbit) {
        try {
            s.setstate(ios_base::badbit); // might throw basic_ios::failure
        }
        catch(...) {
            // ... do nothing ...
        }
        throw; // re-throw
    }
    s.setstate(ios_base::badbit);
}
```

The try-block is needed because setstate() might throw basic_ios::failure (§38.3, §38.4.5.1). However, if badbit is set in the exception state, operator<<() must re-throw the exception that caused handle_ioexception() to be called (rather than simply throwing basic_ios::failure).

The << for a built-in type, such as double, must be implemented by writing directly to a stream buffer. When writing a << for a user-defined type, we can often avoid the resulting complexity by expressing the output of the user-defined type in terms of output of existing types (§39.3.2).

## 39.4.2.3 Numeric Input

When reading from a stream buffer (§38.6), an istream relies on the num_get facet:

num_get<In = istreambuf_iterator<C>> facet (§iso.22.4.2.1)

Read [b:e) into v, using formatting rules from s, reporting errors by setting r

```
In get(In b, In e, ios_base& s, ios_base::iostate& r, bool& v) const;
In get(In b, In e, ios_base& s, ios_base::iostate& r, long& v) const;
In get(In b, In e, ios_base& s, ios_base::iostate& r, long long& v) const;
In get(In b, In e, ios_base& s, ios_base::iostate& r, unsigned short& v) const;
In get(In b, In e, ios_base& s, ios_base::iostate& r, unsigned int& v) const;
In get(In b, In e, ios_base& s, ios_base::iostate& r, unsigned long& v) const;
In get(In b, In e, ios_base& s, ios_base::iostate& r, unsigned long long& v) const;
In get(In b, In e, ios_base& s, ios_base::iostate& r, float& v) const;
In get(In b, In e, ios_base& s, ios_base::iostate& r, double& v) const;
In get(In b, In e, ios_base& s, ios_base::iostate& r, long double& v) const;
In get(In b, In e, ios_base& s, ios_base::iostate& r, void*& v) const;
```

Basically, num_get is organized like num_put (§39.4.2.2). Since it reads rather than writes, get() needs a pair of input iterators, and the argument designating the target of the read is a reference.

The iostate variable r is set to reflect the state of the stream. If a value of the desired type could not be read, failbit is set in r; if the end-of-input was reached, eofbit is set in r. An input operator will use r to determine how to set the state of its stream. If no error was encountered, the value read is assigned through v; otherwise, v is left unchanged.

A sentry is used to ensure that the stream’s prefix and suffix operations are performed (§38.4.1). In particular, the sentry is used to ensure that we try to read only if the stream is in a good state to start with. For example, an implementer of istream might write:

```
template<class C, class Tr>
basic_istream<C,Tr>& basic_istream<C,Tr>::operator>>(double& d)
{
    sentry guard(*this); // see §38.4.1
    if (!guard) return *this;
    iostate state = 0; // good
    istreambuf_iterator<C,Tr> eos;
    try {
        double dd;
        use_facet<num_get<C,Tr>>(getloc()).get(*this,eos,*this,state,dd);
        if (state==0 || state==eofbit)
            d = dd; // set value only if get() succeeded
        setstate(state);
    }
    catch (...) {
        handle_ioexception(*this); // see §39.4.2.2
    }
    return *this;
}
```

I took care not to modify the target of the >> unless the read operation succeeded. Unfortunately, that cannot be guaranteed for all input operations.

Exceptions enabled for the istream will be thrown by setstate() in case of error (§38.3). By defining a numpunct, such as My_punct from §39.4.2.1, we can read using nonstandard punctuation. For example:

```
void f()
{
    cout << "style A: ";
    int i1;
    double d1;
    cin >> i1 >> d1; // read using standard "12345678" format

    locale loc(locale::classic(),new My_punct);
    cin.imbue(loc);
    cout << "style B: ";
    int i2;
    double d2;
```

A simple Money type can be used to control I/O formats or to hold monetary values. In the former case, we cast values of (other) types used to hold monetary amounts to Money before writing, and we read into Money variables before converting them to other types. It is less error-prone to consistently hold monetary amounts in a Money type; that way, we cannot forget to cast a value to Money before writing it, and we don’t get input errors by trying to read monetary values in locale-insensitive ways. However, it may be infeasible to introduce a Money type into a system that wasn’t designed for that. In such cases, applying Money conversions (casts) to read and write operations is necessary.

## 39.4.3.1 Money Punctuation

The facet controlling the presentation of monetary amounts, moneypunct, naturally resembles the facet for controlling plain numbers, numpunct (§39.4.2.1):

```
class money_base {
public:
    enum part { // parts of value layout
        none, space, symbol, sign, value
    };

    struct pattern { // layout specification
        char field[4];
    };
};

template<class C, bool International = false>
class moneypunct : public locale::facet, public money_base {
public:
    using char_type = C;
    using string_type = basic_string<C>;
    // ...
};
```

The moneypunct member functions define the layout of money input and output:

moneypunct<C,International> facet (§iso.22.4.6.3)

| Member | Description/Example |
|---|---|
| `C decimal_point() const;` | E.g., `'.'` |
| `C thousands_sep() const;` | E.g., `','` |
| `string grouping() const;` | E.g., `""` meaning "no grouping" |
| `string_type curr_symbol() const;` | E.g., `"$"` |
| `string_type positive_sign() const;` | E.g., `""` |
| `string_type negative_sign() const;` | E.g., `"-"` |
| `int frac_digits() const;` | Number of digits after `"."`, e.g., `2` |
| `pattern pos_format() const;` | symbol, space, sign, none, or value |
| `pattern neg_format() const;` | symbol, space, sign, none, or value |
| `static const bool intl = International;` | Use three-letter international abbreviations |

The facilities offered by moneypunct are intended primarily for use by implementers of money_put and money_get facets (§39.4.3.2, §39.4.3.3).

A _Bynames version (§39.4, §39.4.1) of moneypunct is provided:

```
template<class C, bool Intl = false>
```
