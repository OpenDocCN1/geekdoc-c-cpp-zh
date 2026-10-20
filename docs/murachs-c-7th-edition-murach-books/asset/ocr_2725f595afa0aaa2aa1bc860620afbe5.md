# The unit testing process

![](bbox=[0.15, 0.11, 0.79, 0.26])

# Advantages of using unit tests

+   - Unit testing helps you find problems earlier in the development cycle than would be possible if you tested all your methods manually.
+   - You can run the unit tests for a class each time you change it to quickly detect any problems that were introduced.
+   - You can develop and test an application more quickly because you don’t have to run the application and retest it each time you change the code. Instead, you can use unit tests to test just the code that was changed without running the application.
+   - Unit testing makes debugging easier because when a test fails, you only need to debug the most recent code changes.

# Description

+   - *Unit testing* provides a way to write code that automatically tests individual methods, called *units*, to verify that they work properly in isolation.
+   - You can use *unit tests* to test the methods in any type of class, including business classes, database classes, and form classes.
+   - You code unit tests within a separate project that’s part of the solution that contains the classes to be tested.
+   - By default, Visual Studio provides for creating three types of test projects for .NET Core applications: MSTest, xUnit, and NUnit. In this chapter, you’ll learn how to use MSTest.