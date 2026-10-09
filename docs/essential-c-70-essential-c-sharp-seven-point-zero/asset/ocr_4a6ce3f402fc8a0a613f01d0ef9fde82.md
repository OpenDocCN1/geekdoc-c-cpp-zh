# **TABLE 5.2: Common Exception Types (continued)**

| Exception Type | Description |
|---|---|
| `System.ArgumentException` | Indicates that one of the arguments passed into the method is invalid. |
| `System.ArgumentNullException` | Indicates that a particular argument is `null` and that this is not a valid value for that parameter. |
| `System.ApplicationException` | To be avoided. The original idea was that you might want to have one kind of handling for system exceptions and another for application exceptions, which, although plausible, doesn't actually work well in the real world. |
| `System.FormatException` | Indicates that the string format is not valid for conversion. |
| `System.IndexOutOfRangeException` | Indicates that an attempt was made to access an array or other collection element that does not exist. |
| `System.InvalidCastException` | Indicates that an attempt to convert from one data type to another was not a valid conversion. |
| `System.InvalidOperationException` | Indicates that an unexpected scenario has occurred such that the application is no longer in a valid state of operation. |
| `System.NotImplementedException` | Indicates that although the method signature exists, it has not been fully implemented. |
| `System.NullReferenceException` | Thrown when code tries to find the object referred to by a reference that is `null`. |
| `System.ArithmeticException` | Indicates an invalid math operation, not including divide by zero. |
| `System.ArrayTypeMismatchException` | Occurs when attempting to store an element of the wrong type into an array. |
| `System.StackOverflowException` | Indicates an unexpectedly deep recursion. |