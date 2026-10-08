As long as we leave the representation of **Date** accessible to everybody, somebody will – by accident or design – mess it up; that is, someone will do something that produces an invalid value. In this case, we created a **Date** with a value that doesn't correspond to a day on the calendar. Such *invalid objects* are time bombs; it is just a matter of time before someone innocently uses the invalid value and gets a run-time error or – usually worse – produces a bad result.

Such concerns lead us to conclude that the representation of **Date** should be inaccessible to users except through the public member functions that we supply. Here is a first cut:

```
```cpp
// simple Date (control access)
class Date {
  int y, m, d;                       // year, month, day
public:
  Date(int y, int m, int d);         // check for valid date and initialize
  void add_day(int n);               // increase the Date by n days
  int month() { return m; }
  int day() { return d; }
  int year() { return y; }
};
```
```

We can use it like this:

```
```cpp
Date birthday {1970, 12, 30};      // OK
birthday.m = 14;                    // error: Date::m is private
cout << birthday.month() << '\n';  // we provided a way to read m
```
```

The notion of a "valid **Date**" is an important special case of the idea of a valid value. We try to design our types so that values are guaranteed to be valid; that is, we hide the representation, provide a constructor that creates only valid objects, and design all member functions to expect valid values and leave only valid values behind when they return. The value of an object is often called its *state*, so the idea of a valid value is often referred to as a *valid state* of an object.

The alternative is for us to check for validity every time we use an object, or just hope that nobody left an invalid value lying around. Experience shows that "hoping" can lead to "pretty good" programs. However, producing "pretty good" programs that occasionally produce erroneous results and occasionally crash is no way to win friends and respect as a professional. We prefer to write code that can be demonstrated to be correct.

A rule for what constitutes a valid value is called an *invariant*. The invariant for **Date** ("A **Date** must represent a day in the past, present, or future") is unusually