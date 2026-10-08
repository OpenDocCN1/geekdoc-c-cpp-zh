# Chapter 10 Classes and Objects: A Deeper Look

+   i) Declaring an instance variable with keyword specifies that the variable is not modifiable.

+   j) The operator returns the string representation of an identifier's name.

+   k) enables you to define how built-in operators work with objects of your own types.

+   l) enable you to add new capabilities to existing types.

10.2 Suppose class Book defines properties Title, Author and Year. Use an object initializer to create an object of class and initialize its properties.

# Answers to Self-Review Exercises

+   10.1 a) services, public interface. b) hides. c) destructor. d) default constructor. e) ToString. f) has-a. g) static. h) principle of least privilege. i) readonly, j) nameof. k) operator overloading.

```
10.2 new Book (Title = "Visual C# How to Program", Author = "Deitel", Year = 2017)
```

# Exercises

10.3 (Hemisphere Class) Create class Hemisphere. The class has an attribute radius which defaults to 1. It has read-only properties that calculate the Volume, CurvedSurfaceArea and TotalArea of the hemisphere. It has properties radius. The accessor should verify that radius is a floating-point number greater than 0 and less than 120.0. Write an app to test Hemisphere.

10.4 (Modifying the Internal Data Representation of a Class) It would be perfectly for the Time2 class of 10.5 to represent the time internally as the number of seconds since midnight rather than the integer values hours, minute and seconds. Clients could use the methods and properties to get the current value. Modify the Time2 class of 10.5 to implement the Time2 as the number of seconds since midnight and show no change is visible to the clients of the class by using the same test app from 10.6.

10.5 (Depreciating Value) Create the class DepreciatingValue. Use the static read-write property DepreciationRate to store the annual depreciation rate for all assets. Each object of the class contains a property ValueAsset which is the current value of the asset. Provide a method CalculateDepreciation to calculate the annual depreciation by multiplying the ValueAsset by AnnualDepreciation—this should be deducted from ValueAsset. Create three DepreciatingValue objects, asset1, asset2 and asset3 with values of $5,000,000, $6,000,000, and $7,000,000 respectively. Set AnnualDepreciationRate to 10%, calculate the ValueAsset for the next three years and display the value for all assets.

10.6 (Enhancing Date Class) Modify class Date of 10.7 to perform error checking on the integer values for variables month and day (Class Date currently validates only the month and day). You'll need to convert the auto-implemented property into instance variable year with an associated Year. Provide method NextDay to increment the day by 1. The Date object should always maintain valid data and throw exceptions when attempts are set to invalid values. Write an app that tests the NextDay method in a loop that displays the dates during each iteration of the loop to illustrate that the NextDay method works correctly. Test the following cases:

+   a) incrementing to the next month

+   b) incrementing to the next year.