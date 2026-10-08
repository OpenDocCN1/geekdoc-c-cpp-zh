We “waste” day[0] to keep the code simple.

```
struct Year {  // a year of temperature readings, organized by month
int year; // positive == A.D.
vector<Month> month {12}; // [0:11] January is 0
};
```

Each class is basically a simple **vector** of “parts”, and **Month** and **Year** have an identifying member **month** and **year**, respectively.

There are several “magic constants” here (for example, **24**, **32**, and **12**). We try to avoid such literal constants in code. These are pretty fundamental (the number of months in a year rarely changes) and will not be used in the rest of the code. However, we left them in the code primarily so that we could remind you of the problem with “magic constants”; symbolic constants are almost always preferable (§7.6.1). Using **32** for the number of days in a month definitely requires explanation; **32** is obviously “magic” here.

Why didn’t we write

```
struct Day {
vector<double> hour {24,not_a_reading};
};
```

That would have been simpler, but unfortunately, we would have gotten a **vector** of two elements (**24** and **–1**). When we want to specify the number of elements for a **vector** for which an integer can be converted to the element type, we unfortunately have to use the ( ) initializer syntax (§18.2).

# 10.11.2 Reading structured values

The **Reading** class will be used only for reading input and is even simpler:

```
struct Reading {
int day;
int hour;
double temperature;
};

istream& operator>>(istream& is, Reading& r)
// read a temperature reading from is into r
// format: ( 3 4 9.7 )
// check format, but don’t bother with data validity
{
```