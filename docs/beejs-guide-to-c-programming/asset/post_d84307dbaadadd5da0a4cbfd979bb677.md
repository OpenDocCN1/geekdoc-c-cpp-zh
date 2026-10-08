
# Chapter 38. Date and Time Functionality

```
// %S: second
// %p: AM or PM
strftime(s, size_of s, "It %I:%M:%S %p", localtime(&now));
puts(s);
// It's 10:20:00 PM

// %F: ISO 8601 year-mm-dd
// %T: ISO 8601 hh:mm:ss
// %z: ISO 8601 time zone offset
strftime(s, size_of s, "ISO 8601: %FT%T%z", localtime(&now));
puts(s);
// ISO 8601: 2021-02-28T22:29:00-0800
```

There are a ton of date printing format specifiers for strftime(), so be sure to check them out in the strftime() reference page.

## 38.5 More Resolution with timespec_get()

You can get the number of seconds and nanoseconds since Epoch with timespec_get(). Maybe.

Implementations might not have nanosecond resolution (that's one billionth of a second) so who knows how many significant places you'll get, give it a shot and see.

timespec_get() takes two arguments. One is a pointer to struct timespec to hold the time information. And the other is the base, the spec lets you set to time_UTC indicating that you're interested in seconds since Epoch. (Other implementations might give you more options for the base) And the structure itself has two fields:

```c
struct timespec {
    time_t tv_sec;   // Seconds
    long tv_nsec;    // Nanoseconds (billions of a second)
};
```

Here's an example where we get the time and print it out as integer values and a floating value:
struct timespec ts;

```c
timespec_get(&ts, TIME_UTC);

printf("%ld %ld ns\n", ts.tv_sec, ts.tv_nsec);

double float_time = ts.tv_sec + ts.tv_nsec/1000000000.0;
printf("%f seconds since epoch\n", float_time);
```

Example output:
161481530, 806326800 ns
161481530.806326 seconds since epoch

struct timespec also makes an appearance in one of the threading functions that need to be able to specify time with that resolution.

> https://beej.us/guide/bgclr/html/split/time.html#man-strftime

## 38.6 Differences Between Times

One quick note about getting the difference between two time_ts: since the spec doesn't dictate how type represents a time, you might not be able to subtract two time_ts and get anything sensible.

Luckily you use difftime() to compute the difference in seconds between two dates.

In the following example, we have two events that occur some time after, and we use difftime() to compute the difference.

```c
#include <stdio.h>
#include <time.h>

int main(void) {
    struct tm time_a = {
        .tm_year=82,      // years since 1900
        .tm_mon=3,         // months since January -- [0, 11]
        .tm_mday=12,       // day of the month -- [1, 31]
        .tm_hour=4,        // hours since midnight -- [0, 23]
        .tm_min=0,         // minutes after the hour -- [0, 59]
        .tm_sec=04,        // seconds after the minute -- [0, 60]
        .tm_isdst=-1,     // Daylight Saving Time flag
    };

    struct tm time_b = {
        .tm_year=120,      // years since 1900
        .tm_mon=10,        // months since January -- [0, 11]
        .tm_mday=15,       // day of the month -- [1, 31]
        .tm_hour=16,       // hours since midnight -- [0, 23]
        .tm_min=27,        // minutes after the hour -- [0, 59]
        .tm_sec=00,        // seconds after the minute -- [0, 60]
        .tm_isdst=-1      // Daylight Saving Time flag
    };

    time_t cal_a = mktime(&time_a);
    time_t cal_b = mktime(&time_b);

    double diff = difftime(cal_b, cal_a);

    double years = diff / 60 / 60 / 24 / 365.2425; // close enough

    printf("%f seconds (%f years) between events\n", diff, years);
}
```

Output:

1217996816.000000 seconds (38.596783 years) between events

Remember to use difftime() to take the time difference. Even though you can just subtract on a POSIX system, it might well stay portable.

# Chapter 39

## Multithreading

C11 introduced, formally, multithreading to the C language. It's very easily similar to POSIX threads¹, if you've ever used those.

And if you've not, no worries. We'll talk it through.

Do note, however, that I'm not intending this to be a full-blown classic multithreading how-to; you'll have to pick up a different very thick book for that, specifically. Sorry!

Threading is an optional feature. If a C11+ compiler defines __STDC_NO_THREADS__, threads will not be present in the library. Whether you decided to go with a negative sense in macro is beyond me, but there we are.

You can test for like it:

```c
#ifdef __STDC_NO_THREADS__
#error I need threads to build this program
#endif
```

Also, you might need to specify certain links when building. In the case of Unix-likes, try appending -lpthreads to the end of the line to link the pthreads library²:

```bash
gcc -std=c11 -o foo foo.c -lpthreads
```

If you're getting linker errors on your, it could be because library wasn't loaded.

### 39.1 Background

Threads are a way to have work in the same program. But more on those later. Let's look at the basics.

### 39.2 Things You Can Do

You can create a thread. It will begin execution on the function you specify.

And you can wait for the thread to complete. This is called joining. Or if you don't care when the thread completes, you can detach. A thread can also explicitly exit by returning from its function. The main() program is a thread, as well.

### 39.3 Data Races and the Standard Library

Some of the functions in the standard library return or use data elements that aren't threadsafe. But in general unless it's said otherwise, the standard library makes an effort to be so.

But keep an eye out. If a thread is maintaining state in a variable you don't own, or if a function is returning a pointer to a thing you didn't pass in, it's unsafe.

### 39.4 Creating and Waiting for Threads

Let's hack something up!

We'll make some threads (create) and wait for them to complete (join).

We have a tiny bit to understand first, though.
Every thread is identified by an opaque variable of type thrd_t. It's a unique identifier for thread in your program. When you create a thread, it's given a new ID.

Also when you make the thread, you have to give it a pointer to a function to run, and a pointer to an argument to pass to it (NULL if you don't have anything to pass).

The thread will begin execution on the function you specify.

So the basic idea is:

-. Write a function to act as the thread's "main". It's not main()-proper, analogous to it. The thread will start running there.
-. From the main thread, launch a new thread with thrd_create(), and pass a pointer to the function to run.
-. In that function, the thread will do whatever it has to do.
-. Meanwhile, the main thread can continue doing whatever it has to do.
- When the main thread decides to exit, it can wait for the child thread to complete by calling thrd_join() the thread to clean up it or else you'll leak memory.

¹https://en.wikipedia.org/wiki/POSIX_threads
²Yes, threading constructs are rusty
³I'm more fan of shared

Unless you use thrd_detach(). More on this later.
