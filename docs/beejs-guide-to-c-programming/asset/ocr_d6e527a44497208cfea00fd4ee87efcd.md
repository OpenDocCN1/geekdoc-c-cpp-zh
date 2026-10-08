# Chapter 38. Date and Time Functionality

Mon Apr 12 12:00:04 1982
Is DST: 0

When you manually load a struct like that, it should be in local time. mktime() will convert that local time into a time_t calendar item.

Weirdly, the standard doesn't give you a way to load a struct tm with a UTC and convert that to a time_t. If you want to do that with Unix-likes, use the non-standard timegm(). On Windows, _mkgmtime().

# 38.4 Formatted Date Output

We've already seen a couple ways to print formatted date to the screen. With time_t we can use ctime(), and with struct tm we can use asctime().

```
time_t now = time(NULL);
struct tm *local = localtime(&now);
struct tm *utc = "UTC" = gmtime(&now);
```

```
printf("Local time: %s\n", ctime(local)); // Local time with time_t
printf("Local time: %s\n", asctime(local)); // Local time with struct tm
printf("UTC: %s\n", asctime(utc)); // UTC with struct tm
```

But what if I told you, dear, there's a way to have more control over how the date was printed?

Sure, we could fetch individual fields out of the struct tm, but there's a great function strftime() that will do all the hard work for you. If it's printf(), except for days!

Let's see some examples. In each of these, we use a destination buffer, a maximum number of characters to write, and a format string (in the style of—but not the same as—printf()) tells strftime() which components of a struct tm to print and how.

You can add other characters to include in the format string, as well, just like with printf().

We get a struct tm in this case from localtime(), but any source works fine.

```
#include <stdio.h>
#include <time.h>
```

```
int main(void) {
  char s[128];
  time_t now = time(NULL);

  // c: print date as per current locale
  strftime(s, sizeof(s), "%c", localtime(&now));
  puts(s); // Sun Feb 28 22:29:00 2021

  // %A: full weekday name
  // %B: full month name
  // %d: day of the month
  strftime(s, sizeof(s), "%A, %B %d", localtime(&now));
  puts(s); // Sunday, February 28

  // %I: hour (12 hour clock)
  // %M: minute
```