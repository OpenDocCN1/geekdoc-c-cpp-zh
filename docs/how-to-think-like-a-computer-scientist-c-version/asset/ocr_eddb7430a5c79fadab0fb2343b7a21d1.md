Time addTime2 (const Time& t1, const Time& t2) {
double seconds = convertToSeconds (t1) + convertToSeconds (t2);
return makeTime (seconds);
}

We have made several changes to this function, including:

+   1. Change the name from addTime to Time::add.
2. Replace the first parameter with an implicit parameter, which should be possible to declared const.
3. Replace the use of makeTime with a constructor invocation.

Here's the result:

```
Time::add (const Time& t2) const {
double seconds = convertToSeconds () + t2.convertToSeconds();
Time time (seconds);
return time;
}
```

The first time we invoke convertToSeconds, there is no apparent object! Inside a member function, the compiler assumes that we want to invoke the function on the current object. Thus, the first invocation acts on this; the second invocation acts on t2.

The next line of the function invokes the constructor that takes a single double as a parameter; the last line returns the resulting object.

# 11.10 Header files

It might seem a nuisance to declare functions inside the structure definition and then define the functions later. Any time you change the interface to a function, you have to change it in two places, even if it is a small change like declaring one of the parameters const.

There is a reason for the hassle, though, which that it is now possible to separate the structure definition and the functions into two files: the header file contains the structure definition, and the implementation file, which contains the functions.

Header files usually have the same name as the implementation file, but with the suffix .h instead of .cpp. For the example we have been looking at, the header file is called Time.h and it contains the following:

```
struct Time {
// instance variables
int hour, minute;
double second;
```