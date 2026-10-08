We put the testing of validity into a separate is_valid() function because checking for validity is logically distinct from initialization and because we might want to have several constructors. As you can see, we can have private functions as well as private data:

```
```
Date::Date(int yy, int mm, int dd)
    : y(yy), m(mm), d(dd)              // initialize data members
{
    if (!is_valid()) throw Invalid{};   // check for validity
}

bool Date::is_valid()                    // return true if date is valid
{
    if (m<1 || 12<m) return false;
    // ...
}
```
```

Given that definition of Date, we can write

```
```
void f(int x, int y)
try {
    Date dxy {2004,x,y};
    cout << dxy << '\n';               // see §9.8 for a declaration of <<
    dxy.add_day(2);
}
catch(Date::Invalid) {
    error("invalid date");              // error() defined in §5.6.3
}
```
```

We now know that << and add_day() will have a valid Date on which to operate. Before completing the evolution of our Date class in §9.7, we’ll take a detour to describe a couple of general language facilities that we’ll need to do that well: enumerations and operator overloading.

# ## 9.5 Enumerations

An enum (an enumeration) is a very simple user-defined type, specifying its set of values (its enumerators) as symbolic constants. For example:

```
```
enum class Month {
    jan=1, feb, mar, apr, may, jun, jul, aug, sep, oct, nov, dec
};
```
```