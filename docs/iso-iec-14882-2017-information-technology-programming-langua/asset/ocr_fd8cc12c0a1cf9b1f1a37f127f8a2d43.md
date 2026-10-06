# ISO/IEC 14882:2017(E)

equals that for another string which does not compare equal should be very small, approaching (1.0/numeric_limits<unsigned long>::max()). end note

# 25.4.4.2 Class template collate_byname [locale::collate_byname]

```
namespace std {
    template<class charT>
    class collate_byname : public collate<charT> {
    public:
        using string_type = basic_string<charT>;

        explicit collate_byname(const charT&, size_t refs = 0);
        explicit collate_byname(const string&, size_t refs = 0);

    protected:
        collate_byname();
    };
};
```

# 25.4.5 The time category [category::time]

+   1 Templates time_get<charT, InputIterator> provide date and time formatting and parsing. All specifications of member functions for time_put and time_get in the subclasses of 25.4.5 apply only to the specifications described in Tables 69 and 70 (25.3.1.1). Their members use ios_base::ios_base::iostate&, and fill arguments as described in 25.4, and the <ctype> facet, to determine formatting details.

# 25.4.5.1 Class template time_get [locale::time_get]

```
namespace std {
    class time_base {
    public:
        enum dateorder {no_number, day, mdy, ydm, ymd};
    };

    template<class charT, InputIterator>
    class time_get : streambuf_iterator<charT>>
    class time_get : public locale::facet, public time_base {
    public:
        using char_type = charT;
        using iter_type = InputIterator;

        explicit time_get(size_t refs = 0);

        dateorder get_order() const { return do_date_order(order_); };
        iter_type get_time(iter_type s, iter_type end, ios_base& f, 
            size_t& err, const ios_base::iostate& err, tm* t) const;
        iter_type get_date(iter_type s, iter_type end, ios_base& f, 
            size_t& err, const ios_base::iostate& err, tm* t) const;
        iter_type get_weekday(iter_type s, iter_type end, ios_base& f, 
            size_t& err, const ios_base::iostate& err, tm* t) const;
        iter_type get_month(iter_type s, iter_type end, ios_base& f, 
            size_t& err, const ios_base::iostate& err, tm* t) const;
        iter_type get_year(iter_type s, iter_type end, ios_base& f, 
            size_t& err, const ios_base::iostate& err, tm* t) const;
        iter_type get_type(iter_type s, iter_type end, ios_base& f, 
            size_t& err, const ios_base::iostate& err, tm* t) const;
        iter_type get_time(iter_type s, iter_type end, ios_base& f);
```