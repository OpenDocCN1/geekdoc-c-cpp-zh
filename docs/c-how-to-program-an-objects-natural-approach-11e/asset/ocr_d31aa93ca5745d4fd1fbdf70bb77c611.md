```
std::cout << "Constructed with:\n\n";
displayTime("t1: all arguments defaulted", t1);
displayTime("t2: hour specified; minute and second defaulted", t2);
displayTime("t3: hour and minute specified; second defaulted", t3);
displayTime("t4: hour, minute and second specified", t4);

// attempt to initialize t5 with invalid values
try {
    const Time t5{27, 74, 99}; // all bad values specified
}
catch (const std::invalid_argument& e) {
    std::cerr << std::format("t5 not created: {}\n", e.what());
}
}
```

```
Constructed with:

t1: all arguments defaulted
24-hour time: 00:00:00
12-hour time: 12:00:00 AM

t2: hour specified; minute and second defaulted
24-hour time: 02:00:00
12-hour time: 2:00:00 AM

t3: hour and minute specified; second defaulted
24-hour time: 21:34:00
12-hour time: 9:34:00 PM

t4: hour, minute and second specified
24-hour time: 12:25:42
12-hour time: 12:25:42 PM

t5 not created: hour was out of range
```

**Fig. 9.12** | Constructor with default arguments. (Part 2 of 2.)

# Software Engineering Notes Regarding Class Time’s Set and Get Functions and Its Constructor

Time’s `set` and `get` functions are called throughout the class’s body. In particular, the constructor (Fig. 9.11, lines 9–11) calls `setTime`, and `to24HourString` and `to12HourString` call `getHour`, `getMinute` and `getSecond` in lines 54 and lines 60–61. We could have accessed the class’s private data in each case directly.

Our internal time representation requires 12 bytes of memory on systems with four-byte ints. Consider changing this to the total seconds since midnight—a single int requiring only four bytes of memory. If we made this change, only the bodies of functions directly accessing the private data would need to change. In this class, we’d modify `setTime` and the `set` function’s bodies for `m_hour`, `m_minute` and `m_second`. There would be no need to modify the constructor or functions `to24HourString` or `to12HourString` because they do not access the data directly.