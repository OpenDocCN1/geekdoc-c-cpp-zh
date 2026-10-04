# 726 Structures

In getVals(), the variable next is defined as a structure of the type to be returned.
After values have been assigned to the next structure, the structure values are returned by including the structure name in the return statement.

On the receiving side, main() must be alerted that the getVals() function will be returning a structure. This alert is handled by including a function declaration for getVals() in main(). Notice that these steps for returning a structure from a function are identical to procedures for returning scalar data types, described in Chapter 6.

![](bbox=[0.106, 0.243, 0.166, 0.313])

# EXERCISES 13.3

+   1. (Data Processing) Write a C++ function named days() that determines the number of days from the turn of the century for any date passed as a structure. Use the Date structure:
```cpp
struct Date
{
    int month;
    int day;
    int year;
};
```
In the days() function, follow the financial convention that all years have 360 days and each month consists of 30 days. The function should return the number of days for any Date passed to it.
2. (Data Processing) Write a C++ function named difDays() that calculates and returns the difference between two dates. Each date is passed to the function as a structure by using the following data type:
```cpp
struct Date
{
    int month;
    int day;
    int year;
};
```
TheDays() function should make two calls to the days() function written for Exercise 1.
3. (Modify) Rewrite the dates for Exercise 1 to receive a reference to a Date structure rather than a copy of the structure.
   b. Redo Exercise 3a, using a pointer rather than a reference.
4. (Data Processing) a. Write a C++ function named larger() that returns the later date of any two dates passed to. For example, if the dates 10/9/2005 and 11/3/2005 are passed to larger(), the second date is returned.
   b. Include the larger() function written for Exercise 4a in a complete program. Store the Date structure returned by larger() in a separate Date structure and display the member values of the returned Date.