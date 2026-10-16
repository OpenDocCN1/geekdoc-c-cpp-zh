A call of **get(b,e,ib,err,pt,fmtb,fmtb)** uses a **strftime()** format presented as a string [**fmtb:fmte**]. This overload, together with the one with the defaulted modifier, does not have **do_get()** interfaces. Instead, they are implemented by calls to the **do_get()** for the first **get()**.

The obvious use of the time and date **facets** is to provide **locale**-sensitive I/O for a **Date** class. Consider a variant of the **Date** from §16.3:

```
class Date {
public:
    explicit Date(int d ={}, Month m ={}, int year ={});
    // …
    string to_string(const locale& = locale()) const;
};
```

```
istream& operator>>(istream& is, Date& d);
ostream& operator<<(ostream& os, Date d);
Date::to_string()
```

produces a **locale()**-specific **string** using a **stringstream** (§38.2.2):

```
string Date::to_string(const locale& loc) const
{
    ostringstream os;
    os.imbue(loc);
    return os << *this;
}
```

Given **to_string()**, the output operator is trivial:

```
ostream& operator<<(ostream& os, Date d)
{
    return os<<to_string(d,os.getloc());
}
```

The input operator needs to be careful about state:

```
istream& operator>>(istream& is, Date& d)
{
    if (istream::sentry guard{is}) {
        ios_base::iostate err = goodbit;
        struct tm t;
        use_facet<time_get<char>>(is.getloc()).get_date(is,0,is,err,&t); // read into t
        if (!err) {
            Month m = static_cast<Month>(t.tm_mon+1);
            d = Date(t.tm_day,m,t.tm_year+1900);
        }
        is.setstate(err);
    }
    return is;
}
```