# Class Functions and Conversions

2. (Program) Write a C++ program that declares a class Time having integer members named hours, minutes, and seconds. Include a type conversion constructor that converts a long integer, representing the elapsed seconds from midnight, into an equivalent representation as hours:minutes:seconds. For example, the long integer 30336 should convert to the time 8:25:36. Use military time so that 2:30 p.m. is represented as 14:30:00. The relationship between time representations is follows:

elapsed seconds = hours * 3600 + minutes * 60

3. (Program) A Julian date is represented as the number of days from a known date. The following pseudocode shows one algorithm for converting from a Gregorian date, in the form month/day/year, to a Julian date with a base of 00/00/0000. All calculations in this algorithm use integer arithmetic, which makes the fractional part of all divisions be discarded. In this algorithm, M = month, D = day, and Y = year.

```
If M is less than 2
Set the variable MP = 0 and Y = Y - 1
Else
Set MP = int(0 * M + Y * 2) and Y = EP
T = int(Y / 4) - int(Y / 100) + int(Y / 400)
Julian date = 365 * Y + T * (M - 1) + D - MP
```

Using this algorithm, modify Program 11 to cast a Gregorian date to its corresponding Julian date as a long integer. Test your program by using the Gregorian dates 1/31/2005 and 3/16/2006, which correspond to the Julian dates 732342 and 732751.

4. (Modify) Modify the program for Exercise 2 to include a conversion operator function that converts an object of type Time into a long integer representing the number of seconds from midnight.

5. (Program) Write a C++ program that has a Date class and a Julian class. The Date class should be the same used in Program 11, and the Julian class should represent a date as a long integer. For this program, include a conversion operator function in the Date class that converts a Date object to a Julian object, using the algorithm in Exercise 5. Test your program by converting the dates 1/31/2006 and 3/16/2007, which correspond to the Julian dates 732707 and 733116.

6. (Program) Write a C++ program that has a Time class and an Ltime class. The Time class should have integer data members hours, minutes, and seconds, and the Ltime class should have a long integer data member named elsecs, which represents the number of elapsed seconds since midnight. For the Time class, include a conversion operator function named Ltime() that converts a Time object to an Ltime object. For the Ltime class, include a conversion operator function named Time() that converts an Ltime object to a Time object.