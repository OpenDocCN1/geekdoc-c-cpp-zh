
# Chapter 38

# Date and Time Functionality

> Time is an illusion. Lunchtime doubly so.
—Ford Prefect, the Hitchhiker's Guide to the Galaxy

This isn't too complex, but it can be a little intimidating at first, both with the different types available and the way we can convert between them.

Mix in time (UTC) and local time and we have all the Usual Fun™ one gets with times and dates.

And of course never forget the golden rule of dates and times: Never attempt to write your own date and time functionality. Only use what the library gives you.

Time is too complex for mortal programmers to handle correctly. Seriously, we all owe a point to everyone who worked on any date and time library, so put that in your budget.

## 38.1 Quick Terminology and Information

Just a quick term in case you don't have them down.

- **UTC**: Coordinated Universal Time is a universally¹ agreed upon, absolute time. Everyone on the planet it's the same right now in UTC... even though they have different offsets.
- **GMT**: Greenwich Mean Time, effectively the same as UTC². You probably want to say UTC, or "universal time". If you're talking specifically about the GMT time zone, say GMT. Confusingly, many of C's functions predict UTC and still refer to Greenwich Mean Time. When you see, that C means UTC.
- **Local time**: what time is where the computer running the program is. This is described as an offset from UTC. There are many time zones in the world, most computers work in either local time or UTC.

As a general rule, if you are describing an event that happens one time, like a log entry, or a rocket launch, or pointers finally clicked for you, use UTC.

On the other hand, if it's something that happens the same time in every time zone, like New Year's Eve or a lot of pain by choosing to store your dates in the wrong form.

Since a lot of languages are only good at converting UTC and local time, you can cause yourself a lot of pain by choosing to store your dates in the wrong form. (Ask me how I.)

> ¹On Earth, anyway knows what crazy systems they are out there...
²OK, don't murder me! GMT is technically a time zone while UTC is a global time system. Some countries might adjust GMT for daylight saving time, whereas UTC is never adjusted for daylight saving time.

## 38.2 Date Types

There are two main types in C when it comes to date: `time_t` and `struct tm`.

The spec doesn't actually say much about them:

- *time_t*: a real type of holding time. By the spec, this could be a floating type or integer type. In POSIX (Unix-likes), it's an integer. This holds calendar time, which you can think of as UTC.
- *struct tm*: the components of a calendar time. This is a broken-down time, i.e. components of the time like hour, minute, second, day, month, year, etc.

On a lot of systems, `time_t` represents the number of seconds since Epoch. Epoch is some time from the computer's perspective, which is commonly January 1, 1970. `time_t` can go negative to represent times before Epoch. Windows behaves differently.

And what's in `struct tm`? The following fields:

```c
struct tm {
    int tm_sec;  // seconds after the minute [0, 60]
    int tm_min;  // minutes after the hour [0, 59]
    int tm_hour; // hours since midnight [0, 23]
    int tm_mday;  // day of the month [1, 31]
    int tm_mon;   // months since January [0, 11]
    int tm_year;  // years since 1900
    int tm_wday;  // days since Sunday [0, 6]
    int tm_yday;  // days since January [0, 365]
    int tm_isdst;// Daylight Saving Time flag
};
```

Everything is zero-based except the day of the month. It's important to know that you can put any values in these types. There are functions to help get the time now.

So the question becomes: "How do you initialize these types, and how do you convert between them?"

## 38.3 Initialization and Conversion

First, you can get the current time and store it in a `time_t`.

```c
time_t now; // Variable to hold the time
now = time(NULL); // You can get it like this
time(&now); // ... Same as the previous line.
```

Great! You have a variable that gets you the time now. Strang, there's only one portable way to print what's in a `time_t`, and that's the rarely-used `ctime` function that prints the value in local time:

```c
now = time(NULL);
printf("%s", ctime(now));
```

This returns a string with a very specific form that includes a newline at the end:

> ³Actually, there are more than two.
>⁴https://en.wikipedia.org/wiki/Unix_time

So that `time_t` is a kind of inflexible. If you want more control, you should convert `time_t` into a `struct tm`.

### 38.3.1 Converting time_t to struct tm

There are two amazing ways to do this conversion:

- `localtime()`: this function converts a `time_t` to a `struct tm` in local time.
- `gmtime()`: this function converts a `time_t` to a `struct tm` in UTC.

Let's see what it is by printing out a `struct tm` with the `asctime()` function:

```c
printf("Local: %s", asctime(local));
```

Output (I'm in the Pacific Standard Zone):
Local: Sun Feb 28 20:15:27 2021
UTC: Mon Mar 1 04:15:27 2021

Once you have your `time_t` in a struct, it opens all kinds of doors. You can print out the time in a variety of ways, figure out which day of the week it is, and so on. Or convert it back into a `time_t`.

More on that soon!

### 38.3.2 Converting struct tm to time_t

If you want to go the other way, you can use `mktime()` to get information.

`mktime()` sets the values of `tm_wday` and `tm_yday` for you, so don't bother them out because they'll be overwritten.

Also, you can set `tm_isdst` to -1 to make it have the determination for you. Or you can manually set it to true or false.

```c
// Don't be tempted to put leading zeros on these numbers (unless
// mean for them to be in time!)
```

```c
struct tm some_time_t = {
  .tm_year=82, // years since 1900
  .tm_mon=3,   // months since January [0, 11]
  .tm_day=12,  // day of the month [1, 31]
  .tm_hour=12, // hours since midnight [0, 23]
  .tm_min=0,   // minutes after the hour [0, 59]
  .tm_sec=4,   // seconds after the minute [0, 60]
  .tm_isdst=-1, // Daylight Saving Time flag
};

time_t some_time_t_epoch;
some_time_epoch = mktime(&some_time_t);

```c
printf("%s", ctime(&some_time_epoch));
printf("Is DST: %d\n", some_time_t.tm_isdst);
```

Output:
Mon Apr 1 12:00:04 1982
Is DST: 0

## 38.4 Formatted Date Output

We've already seen a couple of ways to print formatted date. With `time_t` we can use `ctime()`, and with `struct tm` we can use `asctime()`.

But what if I told you, dear, there's a way to have more control over how the date was?

Sure, we could fetch individual fields out of the `struct tm`, but there's a great function `strftime()` that will do all the hard work for you. In each of these, we use a destination buffer, a maximum number of characters to write, and a format string (in the style of—but not the same as—printf()) tells `strftime()` which components of a `struct tm` to print and how.

We get a struct tm in this case from `localtime()`, but any source works fine.
