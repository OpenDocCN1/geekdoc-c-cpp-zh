```
//Place the definitions of the remaining functions, getTime,
//incrementHours, incrementMinutes, incrementSeconds, printTime,
//and equalTime, of the class clockType, as described
//previously here.
```

**Sample Run:** In this sample run, the user input is shaded.

```
Line 2: myClock: 05:04:30
Line 5: yourClock: 0-858993460-0-858993460-0-858993460
Line 9: After setting yourClock: 05:45:16
Line 15: The two times are not equal.
Line 16: Enter the hours, minutes, and seconds: 5 23 59

Line 20: New myClock: 05:23:59
Line 24: After incrementing myClock by one second, myClock: 05:24:00
Line 28: hours = 5, minutes = 24, seconds = 0
```

The value of yourClock, as printed in the second line of the output (Line 5), is machine dependent—you might get different values.

# ## Order of public and private Members of a Class

C++ has no fixed order in which you declare public and private members; you can declare them in any order. The only thing you need to remember is that, by default, all members of a class are private. You must use the member access specifier `public` to make a member available for public access. If you decide to declare the private members after the public access specifier (as is done in the case of clockType), you must use the member access specifier `private` to begin the declaration of the private members.

We can declare the class clockType in one of three ways, as shown in Examples 10-3 through 10-5.

# EXAMPLE 10-3

This declaration is the same as before. For the sake of completeness, we include the class definition:

```
class clockType
{
public:
    void setTime(int, int, int);
    void getTime(int&, int&, int&) const;
    void printTime() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&) const;
```