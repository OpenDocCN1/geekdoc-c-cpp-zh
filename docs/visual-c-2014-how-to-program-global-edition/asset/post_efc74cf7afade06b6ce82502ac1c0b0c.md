
# 464 Chapter 10 Classes and Objects: A Deeper Look

| 25 | Console.WriteLine({x} + {y} = {x + y}); |
| 26 | Console.WriteLine({x} - {y} = {x - y}); |
| 27 | Console.WriteLine({x} * {y} = {x * y}); |
| 28 | } |

Enter the real part of complex number x: 2
Enter the imaginary part of complex number x: 4
Enter the real part of complex number y: 4
Enter the imaginary part of complex number y: -2

```
(2 + 4i) + (4 - 2i) = (6 + 2i)
(2 + 4i) - (4 - 2i) = (-2 + 6i)
(2 + 4i) * (4 - 2i) = (16 + 12i)
```

> Fig. 10.15 | Overloading operators for complex numbers. (Part 2 of 2.)

Lines 25–27, add, subtract and multiply x and y with the overloaded operators (in string-interpolation expressions), then output the results. In line 25, we use the + operator for ComplexNumber operands x and y. Without operator overloading, x+y would make sense—the compiler would know how to add two ComplexNumber objects. This expression makes sense here because we've defined the + operator for two ComplexNumbers System in lines 24–28 of Fig. 10.14. When the two ComplexNumbers are “added” in line 25 of 10.15, this invokes the operator declaration, leaving the left operand as the first argument and the right operand as the second argument. When we use the subtraction and multiplication operators in lines 26–27, their respective overloaded operator declarations are invoked implicitly.

Each calculation's result is the new ComplexNumber returned by the corresponding overloaded operator method. When this object is placed in a string-interpolation expression, its ToString method (Fig. 10.14, lines 20–21) is implicitly invoked. The expression x+y in line 25 of 10.15 could be rewritten to explicitly invoke the ToString method of the resulting ComplexNumber object, in:

```
(x + y).ToString()
```

## 10.14 Time Class Study: Extension Methods

You can use extension methods to add functionality to an existing type without modifying the type. You saw in Section 9.3 that LINQ’s capabilities are implemented as extension methods. Figure 10.16 uses extension methods to add two new methods to class (Section 10.5)—DisplayTime and AddHours.

```csharp
// Fig. 10.16: TimeExtensions.cs
// Demonstrating extension methods.
using System;
class TimeExtensions
{
```

> Fig. 10.16 | Demonstrating extension methods. (Part 1 of 2.)

## 10.14 Time Class Study: Extension Methods

```csharp
static void Main()
{
    var myTime = new Time2(); // call Time2 constructor
    myTime.Set(11, 34, 15); // set the time to 11:34:15

    // test the DisplayTime method
    Console.Write("Use DisplayTime method: ");
    myTime.DisplayTime();

    // test the AddHours method
    Console.Write("Add 5 hours with AddHours method: ");
    var timeAdded = myTime.AddHours(5); // add five hours
    timeAdded.DisplayTime(); // display the new Time2 object

    // add hours and display the time in statement
    Console.Write("Add 15 hours with AddHours method: ");
    myTime.AddHours(15).DisplayTime(); // add hours and display time

    // use fully qualified method name to display the time
    Console.Write("Use fully qualified method name: ");
    TimeExtensions.DisplayTime(myTime);
}

// extension methods class
static class TimeExtensions
{
    // display the Time2 object in console
    public static void DisplayTime(this Time2 aTime)
    {
        Console.WriteLine(aTime.ToString());
    }

    // add the specified number of hours to the time
    // and return a new Time2 object
    public static Time2 AddHours(this Time2 aTime, int hours)
    {
        // create a new Time2 object
        var newTime = new Time2()
        {
            Minute = aTime.Minute,
            Second = aTime.Second
        };
        // add the specified number of hours to the given time
        newTime.Hour = (aTime.Hour + hours) % 24;

        return newTime; // return the new Time2 object
    }
}
```

| The DisplayTime method: 11:34:15 AM |
| Add 5 hours with AddHours method: 4:34:15 PM |
| Add 15 hours with AddHours method: 23:34:15 AM |
| Use fully qualified method name: 11:34:15 AM |

> Fig. 10.16 | Demonstrating extension methods. (Part 2 of 2.)

# 466 Chapter 10 Classes and Objects: A Deeper Look

### Extension Method DisplayTime

The extension method DisplayTime (lines 35–38) displays the string representation of the time in the console. The new feature of method DisplayTime is the this keyword that precedes the Time parameter in the method header (line 35)—this notifies the compiler that DisplayTime is an extension method for an existing class (Time2). The type of extension method's first parameter specifies the type of object on which you can call the method—therefore each extension method must define at least one parameter. Also, extension methods must be defined as static methods in a static class such as TimeExtensions (lines 32–53). A static class can contain only static members and cannot be instantiated.

### Calling Extension Method DisplayTime

Line 45 uses Time2 myTime to call the DisplayTime extension method. Note that we do not provide an argument to the method call. The compiler implicitly passes the object to method(myTime) as the method's first argument. This allows you to call DisplayTime as if it were a Time2 instance method. In fact, IntelliSense displays extension methods with the class's instance and identifies them with a distinct icon.

The down-arrow in the icon denotes an extension method. Also, when you select an extension method in the IntelliSense window, the tooltip describes the method includes the text (extension) for each extension method.

### Extension Method AddHours

Lines 42–52 of 10.16 declares the AddHours extension method. Again, this keyword in the first parameter's declaration indicates that AddHours can be called on a Time2 object. The second parameter is an int value specifying the number of hours to add to the time. The AddHours method returns a new Time2 object with the specified number of hours added.

Lines 45–46 create the new Time2 object and use an initializer to set its Minute and Second properties to the corresponding values in the parameter atTime—these are not modified when we add hours to the time. Line 49 adds the second argument's number of hours to the original Time2 object's Hour property, then uses the % operator to ensure the value remains in the range 0–23. The result is assigned to the new Time2 object's Hour property. Line 51 returns the new Time2 object to the caller.

### Calling Extension Method AddHours

Line 18 calls the AddHours extension method to add five hours to the myTime object's hour value. Note that the method specifies only one argument—the number of hours to add. Again, the compiler implicitly passes the object used to call the method.

### Calling Both Extension Methods in a Single Statement

Line 23 uses both extension methods in a single statement. Multiple method calls in the same statement are known as cascaded method calls. When a method returns an object, you can follow the method call with a member access operator. In line 23, DisplayTime is called on the object returned by AddHours. to a separate statement.

### Calling an Extension Method With Fully Qualified Name

Line 27 calls DisplayTime using its fully qualified name—name of the class in which the extension method is defined (TimeExtensions), followed by the member access operator ( the method name (DisplayTime) and its argument list. In line 27 the call passes Time2 as an argument. Using the fully qualified name, you must specify an argument for extension method's first parameter.

### Extension Method Cautions

If you declare an extension method already defines an instance method with a compatible signature, the instance method will shadow (i.e., hide) the extension method. Also, if a predefined type is later updated to include an instance method that shadows an extension method, the compiler does not report any errors and the extension method does not appear in IntelliSense.
