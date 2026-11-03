```
Constructed with:
 t1: all arguments defaulted
 00:00:00
 12:00:00 AM

 t2: hour specified; minute and second defaulted
 02:00:00
 2:00:00 AM

 t3: hour and minute specified; second defaulted
 21:34:00
 9:34:00 PM

 t4: hour, minute and second specified
 12:25:42
 12:25:42 PM

 Exception while initializing t5: hour must be 0-23
```

Fig. 17.6 | Constructor with default arguments. (Part 2 of 2.)

# Notes Regarding Class Time's Set and Get Functions and Constructor

Time's set and get functions are called throughout the class's body. In particular, function setTime (lines 16–21 of Fig. 17.5) calls functions setHour, setMinute and setSecond, and functions printUniversal and printStandard call functions getHour, getMinute and getSecond in line 71–72 and lines 78–80. In each case, these functions could have accessed the class's private data directly. However, consider changing the representation of the time from three int values (requiring 12 bytes of memory on systems with four-byte ints) to a single int value representing the total number of seconds that have elapsed since midnight (requiring only four bytes of memory). If we made such a change, only the bodies of the functions that access the private data directly would need to change—in particular, the individual set and get functions for the hour, minute and second. There would be no need to modify the bodies of functions setTime, printUniversal or printStandard, because they do not access the data directly. Designing the class in this manner reduces the likelihood of programming errors when altering the class's implementation.

Similarly, the Time constructor could be written to include a copy of the appropriate statements from function setTime. Doing so may be slightly more efficient, because the extra call to setTime is eliminated. However, duplicating statements in multiple functions or constructors makes changing the class's internal data representation more difficult. Having the Time constructor call setTime and having setTime call setHour, setMinute and setSecond enables us to limit the changes to code that validates the hour, minute or second to the corresponding set function. This reduces the likelihood of errors when altering the class's implementation.

# Software Engineering Observation 17.6

![](bbox=[0.18, 0.95, 0.25, 0.99])

> If a member function of a class already provides all or part of the functionality required by a constructor (or other member function) of the class, call that member function from the constructor (or other member function). This simplifies the maintenance of the code and reduces the likelihood of an error if the implementation of the code is modified. As a general rule: Avoid repeating code.