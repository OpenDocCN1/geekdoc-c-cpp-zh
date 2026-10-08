Chapter 38. Date and Time Functionality

# 38.2 Date Types

There are two main types in C when it comes to date: time_t and struct tm.

The spec doesn't actually say much about them:

+   * time_t: a real type of holding time. By the spec, this could be a floating type or integer type. In POSIX (Unix-likes), it's an integer. This holds calendar time. Which you can think of as UTC time.
* struct tm: the components of a calendar time. This is a broken-down time, i.e. the components of the time, like hour, minute, second, day, month, year, etc.

On a lot of systems, time_t represents the number of seconds since Epoch. Epoch is in some ways the time from the computer's perspective, which is commonly January 1, 1970 UTC. time_t can go negative to represent times before Epoch. Windows behaves the same as Unix from what I can tell you.

And what's in struct tm? The following fields:

```
struct tm {
int tm_sec; // seconds after the minute -- [0, 60]
int tm_min; // minutes after the hour -- [0, 59]
int tm_hour; // hours since midnight -- [0, 23]
int tm_mday; // day of the month -- [1, 31]
int tm_mon; // months since January -- [0, 11]
int tm_year; // years since 1900
int tm_wday; // days since Sunday -- [0, 6]
int tm_yday; // days since January 1 -- [0, 365]
int tm_isdst; // Daylight Saving Time flag
};
```

That everything is zero-based except the day of the month.

It's important to know that you can put any values in these types you want. There are functions to help get the time now, but they hold a time, not the time.

So the question becomes: "How do you initialize data of these types, and how do you convert between them?"

# 38.3 Initialization and Conversion Between Types

First, you can get the current time and store it in a time_t with the time() function.

time_t now; // Variable to hold the time now

now = time(NULL); // You can get it like this...

time(&now); // ... or .. Same as the previous line.

Great! You have a variable that gets you the time now.

Amusingly, there's only one portable way to print what's in a time_t, and that's the rarely-used ctime function that prints the value in local time:

```
now = time(NULL);
printf("%s", ctime(now));
```

This returns a string with a very specific form that includes a newline at the end:

> ³Admitted, there are more than two.

> ⁴https://en.wikipedia.org/wiki/Unix_time