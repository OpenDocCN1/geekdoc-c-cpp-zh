# Adding Functionality to Your Classes

```
```cpp
{
    private:
        long yyyymmdd;
    public:
        Intdate(long ym = 0);    // constructor
        operator Date();          // conversion operator from Intdate to Date
        void showint();
};
```
```

```
```cpp
// class implementation section for Date
Date::Date(int mm, int dd, int yyyy)  // constructor
{
    month = mm;
    day = dd;
    year = yyyy;
}
```
```

```
```cpp
// conversion operator function converting from Date to Intdate class
Date::operator Intdate()    // must return an Intdate object
{
    long temp;
    temp = year * 10000 + month * 100 + day;
    return(Intdate(temp));
}
```
```

```
```cpp
// member function to display a Date
void Date::showDate()
{
    cout << setfill('0')
         << setw(2) << month << '/'
         << setw(2) << day << '/'
         << setw(2) << year % 100;
    return;
}
```
```

```
```cpp
// class implementation section for Intdate
Intdate::Intdate(long ymd)  // constructor
{
    yyyymmdd = ymd;
}
```
```

```
```cpp
// conversion operator function converting from Intdate to Date class
Intdate::operator Date()    // must return a Date object
```
```