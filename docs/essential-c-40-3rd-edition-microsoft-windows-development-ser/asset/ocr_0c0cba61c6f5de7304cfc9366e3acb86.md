is preferable, however, to include a catch block that is specific to the most derived type (System.FormatException, for example), because then it is possible to get the most information about an exception and handle it less generically. In so doing, the catch statement that uses the most derived type is able to handle the exception type specifically, accessing data related to the exception thrown, and avoiding conditional logic to determine what type of exception occurred.

This is why C# enforces that catch blocks appear from most derived to least derived. For example, a catch statement that catches System.Exception cannot appear before a statement that catches System.FormatException because System.FormatException derives from System.Exception.

A method could throw many exception types. Table 4.2 lists some of the more common ones within the framework.

# TABLE 4.2: Common Exception Types

| Exception Type | Description |
| :--- | :--- |
| System.Exception | A generic exception from which other exceptions derive. |
| System.ArgumentException | A means of indicating that one of the parameters passed into the method is invalid. |
| System.ArgumentNullException | Indicates that a particular parameter is null and that this is not valid for that parameter. |
| System.ApplicationException | To be avoided. Originally the idea that you might want to have one kind of handling for "system" exceptions and another for "application" exceptions, although plausible, doesn't actually work well in the real world. |
| System.FormatException | Indicates that the string format is not valid for conversion. |
| System.IndexOutOfRangeException | Indicates that an attempt was made to access an array element that does not exist. |