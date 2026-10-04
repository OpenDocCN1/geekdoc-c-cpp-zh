# Chapter 10 573 Constructors

```
int main()
{
    Date a, b(4,1,1998), c(2006051L); // declare three objects
    a.showDate(); // display object a's values
    b.showDate(); // display object b's values
    c.showDate(); // display object c's values

    return 0;
}
```

Three objects are created in the Program 10.3 main() function. The first object, a is initialized with the default constructor, using its default arguments. Object b is also initialized with the default constructor, using the arguments 4, 1, and 1998. Object c, which is initialized with a long integer, uses the second constructor in the class implementation. The compiler knows to use this second constructor because the argument 2006051L is designated as a long integer by the uppercase L. It's worth pointing out that a compiler error would occur if Date constructors had default values. For example, a declaration as Date d would be ambiguous because the compiler couldn't determine which constructor to use. Therefore, in each implementation section, only one constructor can be written as the default.

As mentioned, constructors can also be written as inline functions. Doing simply defining the function in the class declaration section. For example, the following declaration section makes both constructors in Program 10.3 inline:

```
// class declaration
class Date
{
private:
    int month;
    int day;
    int year;
public:
    Date(int mm = 7, int dd = 4, int yyyy = 2005)
{
        month = mm;
        day = dd;
        year = yyyy;
    }
    Date(long yyyymmmdd) // here is the overloaded constructor
{
    year = int(yyyymmmdd / 10000.0); // extract the year
    // extract the month
    month = int((yyyymmmdd - year * 10000.0) / 100.0);
    // extract the day
    day = int((yyyymmmdd - year * 10000.0 - month * 100.0);
}
}
```