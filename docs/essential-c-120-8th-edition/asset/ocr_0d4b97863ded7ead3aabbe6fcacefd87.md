# Basic Error Handling with Exceptions

TABLE 5.2: Common Exception Types (continued)

| Exception Type | Description |
| --- | --- |
| System.FormatException | Indicates the string format is not valid for conversion. |
| System.IndexOutOfRangeException | Indicates that an attempt was made to access an array or other collection element that does not exist. |
| System.InvalidCastException | Indicates that an attempt to convert from one data type to another was not a valid conversion. |
| System.InvalidOperationException | Indicates that an unexpected scenario has occurred such that the application is no longer in a valid state of operation. |
| System.NotImplementedException | Indicates that although the method signature exists, it has not been fully implemented. |
| System.NullReferenceException | Thrown when code tries to find the object referred to by a reference that is null. |
| System.ArithmeticException | Indicates an invalid math operation, not including divide by zero. |
| System.ArrayTypeMismatch | Occurs when attempting to store an element of the wrong type into an array. |
| System.OverflowException | Indicates an unexpectedly deep recursion |

# ADVANCED TOPIC

# General Catch

It is possible to specify a catch block that takes no parameters, as shown in Listing 5.29.

LISTING 5.29: General Catch Blocks

```
// A previous catch clause already catches all exceptions
#pragma warning disable CS1058
// ...
    try
```