# CHAPTER 1 Data Abstraction: The Walls

the program's side of the wall, you will see an interface that enables you to communicate with the data structure. That is, you use the ADT operations to manipulate the data in the data structure, and you pass the results of these manipulations back to.

Using ADT is like using a vending machine

This process is analogous to using a vending machine. You press buttons to communicate with the machine and obtain something in return. Much as an ADT's specifications dictate what its operations are and what they do. As long as you use a vending machine according to its design, you can ignore its inner technology. As long as you agree access data only by using ADT operations, your program will be oblivious to any change in the data structures that implement the ADT.

The following pages describe several abstract data types, focusing on the specifications of their, but not their implementations.

![](bbox=[0.068, 0.303, 0.205, 0.365])

# 1.4.1 Designing an ADT

The design of an abstract data type should evolve naturally during the problem-solving process. As an example of how this might occur, suppose that you want to determine the dates of all holidays in a year. One way to do this is to examine a calendar. That is, you could consider each day in the year and ascertain whether day is a holiday. The following pseudocode is a possible solution:

```
// Displays the dates of all holidays in a given year.
listHolidays(year)
date = first day of year
while (date is before the first day of year + 1)
{
  if (date is a holiday)
    write(date, "is a holiday")
  date = date of next day
}
```

What data does a problem require?

What is involved here? Clearly, this problem operates on dates, where a date consists of a month, day, and year. What operations will you need to solve the holiday problem? Your ADT specify and restrict the legal operations on the dates, as the fundamental data type int restricts to operations as addition and comparison. You can see from the previous pseudocode that you must

What operations does a problem require?

+   * Determine the date of the first day of a given year.
* Determine whether a date is before another date.
* Determine whether a date is a holiday.
* Determine the date of the day that has a given date.

Thus, you could specify the following operations for an ADT in pseudocode that uses the notation of the Unified Modeling Language (UML), as described in Appendix C:

```
// Returns the date of the first day of a given year.
+getFirstDay(year: integer): Date

// Returns true if this date is before the given date; otherwise returns false.
+isBefore(otherDate: Date): boolean

// Returns true if this date is a holiday; otherwise returns false.
+isHoliday(): boolean

// Returns the date of the day after this date.
+getNextDay(): Date
```