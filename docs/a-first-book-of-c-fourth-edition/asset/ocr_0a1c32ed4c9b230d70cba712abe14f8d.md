results. Notice, too, the forward declaration of the IntDate class before the Date class's declaration. It's required so that the Date class can reference IntDate in its conversion operator function.

# EXERCISES 11.3

+   1. (For review) a. Define the three new data type conversions introduced in this section and the method of performing each conversion.
+   b. Define the terms "type conversion constructor" and "conversion operator function" and describe how they're used in user-defined conversions.

+   2. (Program) Write a C++ program that declares a class named Time having integer data members hours, minutes, and seconds. Include a type conversion constructor that converts a long integer, representing the elapsed seconds from midnight, into an equivalent representation as hours:minutes:seconds. For example, the long integer 30336 should convert to the time 8:25:36. Use military time—for example, 2:30 p.m. is represented as 14:30:00. The relationship between time representations is as follows:
+   elapsed seconds = hours × 3600 + minutes × 60 + seconds

+   3. (Program) A Julian date is represented as the number of days from a known base date. The following pseudocode shows one algorithm for converting from a Gregorian date, in the form month/day/year, to a Julian date with a base date of 00/00/0000. All calculations in this algorithm use integer arithmetic, which means the fractional part of all divisions must be discarded. In this algorithm, M = month, D = day, and Y = year.
+   If M is less than or equal to 2
+   Set the variable MP = 0 and YP = Y - 1
+   Else
+   Set MP = int(0.4 × M + 2.3) and YP = Y
+   EndIf
+   T = int(YP / 4) - int(YP / 100) + int(YP / 400)
+   Julian date = 365 × Y + 31 × (M - 1) + D + T - MP
+   Using this algorithm, modify Program 11.7 to cast from a Gregorian Date object to its corresponding Julian representation as a long integer. Test your program by using the Gregorian dates 1/31/2011 and 3/16/2012, which correspond to the Julian dates 734533 and 734943.

+   4. (Modify) Modify the program written for Exercise 2 to include a conversion operator function that converts an object of type Time into a long integer representing the number of seconds from midnight.

+   5. (Program) Write a C++ program that has a Date class and a Julian class. The Date class should be the same Date class used in Program 11.6, and the Julian class should represent a date as a long integer. For this program, include a conversion operator function in the Date class that converts a Date object to a Julian object, using the algorithm shown in Exercise 3.