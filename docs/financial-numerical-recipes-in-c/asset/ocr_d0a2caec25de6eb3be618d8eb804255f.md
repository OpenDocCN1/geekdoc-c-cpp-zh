# 1.3.1 date, an example class

Consider the abstract concept of a date. A date can be specified in any number of ways. Let us limit ourselves to the Gregorian calendar. 12 august 2003 is a common way of specifying a date. However, it can also be represented by the strings: "2003/8/12", "12/8/2003" and so on, or by the number of years since 1 january 1900, the number of months since January, and the day of the month (which is how a UNIX programmer will think of it).

However, for most people writing programs the representation of a date is not relevant, they want to be able to enter dates in some abstract way, and then are concerned with such questions as:

+   - Are two dates equal?
+   - Is one date earlier than another?
+   - How many days is it between two dates?

A C++ programmer will proceed to use a class that embodies these uses of the concept of a date. Typically one will look around for an extant class which has already implemented this, but we will show a trivial such date class as an example of how one can create a class.

```
class date {
protected:
    int year_;
    int month_;
    int day_;
public:
    date():;
    date(const int& d, const int& m, const int& y);
    bool valid() const;
    int day() const;
    int month() const;
    int year() const;
    void set_day (const int& day );
    void set_month( const int& month );
    void set_year( const int& year );
    date operator ++(); // prefix
    date operator ++(int); // postfix
    date operator --(); // prefix
    date operator --(int); // postfix
};

bool operator == (const date&, const date&); // comparison operators
bool operator != (const date&, const date&);
bool operator < (const date&, const date&);
bool operator > (const date&, const date&);
bool operator <= (const date&, const date&);
bool operator >= (const date&, const date&);
```

# Header file 1.1: Defining a date class

A class is defined in a header file, as shown in Header file 1.1. As internal representation of the date is chosen the three integers day_, month_ and year_. This is the data structure which is then manipulated by the various functions defined below.

The functions are used to