# 11.3 Data Type Conversions

```
day = pt->day;
month=pt->month;
year = pt->year;

return;
}
```

+   b. Include the `addSixMonths()` method given in Exercise 6a in Program 11.5 and verify your answer to Exercise 6a.
+   
+   7. **(Modify)** a. Modify the `addSixMonths()` method given in Exercise 6a to use a reference argument rather than a pointer.
+      b. Include the `addSixMonths()` method written for Exercise 7a in Program 11.5 and verify that this method works as expected.
+   
+   8. **(Modify)** a. Modify the `addSixMonths()` method given in Exercise 6a so that it doesn’t alter the data values in the passed object. Do this by passing a copy of `oldDate` (rather than a pointer or a reference) to the method.
+      b. Include the `addSixMonths()` method written for Exercise 8a in Program 11.5 and verify that this method works as expected.

You have already seen the conversion from one built-in data type to another (see Sections 3.1 and 3.3). With the introduction of classes, there are now three new conversion possibilities:

+   - Conversion from a class type to a built-in type
+   - Conversion from a built-in type to a class type
+   - Conversion from a class type to a class type

Clearly, a conversion makes sense only when there’s a meaningful relationship between data types. The Date class is used in this section to explain these conversions because a useful relationship does exist between a Date object consisting of day, month, and year variables and an integer in the form yyyymmdd. For example, a date such as 9/15/2012 can be represented by the integer 20120915. Dates represented in this manner, as integers, are useful for sorting and comparing dates. Because integers representing dates can exceed the size of a normal integer, long integers are used, as shown in Figure 11.5.