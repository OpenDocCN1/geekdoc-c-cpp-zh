# 466 Chapter 10 Classes and Objects: A Deeper Look

# Extension Method DisplayTime

The extension method DisplayTime (lines 35–38) displays the string representation of the time in the console window. The new feature of method DisplayTime is this keyword that precedes the Time parameter in the method header (line 35)—this notifies the compiler that DisplayTime is an extension method for an existing class (Time2). The type of extension method's first parameter specifies the type of object on which you can call the method—for reason, each extension method must define at least one parameter. Also, extension methods must be defined as static methods in a static class such as TimeExtensions (lines 32–53). A static class can contain only static members and cannot be instantiated.

# Calling Extension Method DisplayTime

Line 145 uses Time2 myTime to call the DisplayTime extension method. Note that we do not provide an argument to the method call. The compiler implicitly passes the object to calls method(myTime) as the method's first argument. This allows you to call DisplayTime as if it were a Time2 instance method. In fact, IntelliSense displays extension methods with the class's instance and identifies them with a distinct icon

The down-arrow in the icon denotes an extension method. Also, when you select an extension method in the IntelliSense window, the tool tip describes the method includes the text (extension) for each extension method.

# Extension Method AddHours

Lines 42–52 of 10.16 declares the AddHours extension method. Again, this keyword in the first parameter's declaration indicates that AddHours can be called on a Time2 object. The second parameter is an int value specifying the number of hours to add to the time. The AddHours method returns a new Time2 object with the specified number of hours added.

Lines 45–46 create the new Time2 object and use an initializer to set its Minute and Second properties to the corresponding values in the parameter atTime—these are not modified when we add hours to the time. Line 49 adds the second argument's number of hours to the original Time2 object's Hour property, then uses the % operator to ensure the value remains in the range 0–23. The result is assigned to the new Time2 object's Hour property. Line 51 returns the new Time2 object to the caller.

# Calling Extension Method AddHours

Line 18 calls the AddHours extension method to add five hours to the myTime object's hour value. Note that the method specifies only one argument—the number of hours to add. Again, the compiler implicitly passes the object's used to call the method(myTime) as the method's first argument. The Time2 object returned by AddHours is assigned to a local variable (timeAdded) and displayed in the console with the DisplayTime extension method (line 19).

# Calling Both Extension Methods in a Single Statement

Line 23 uses both extension methods DisplayTime(myTime and AddHours) in a single statement to add 15 hours to the original myTime and display the result in the console. Multiple