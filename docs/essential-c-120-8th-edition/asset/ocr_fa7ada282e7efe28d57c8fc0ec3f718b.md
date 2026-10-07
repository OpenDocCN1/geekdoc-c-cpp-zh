280 Chapter 5: Parameters and Methods

# ADVANCED TOPIC

# Exception Class Inheritance

All objects thrown as exceptions derive from System.Exception. (Objects thrown from other languages that do not derive from System.Exception are automatically "wrapped" by an object that derives.) Therefore, they can be handled by the catch(System.Exception exception) block. It is preferable, however, to include a block that is specific to the most derived type (e.g., System.FormatException), because then it is possible to get the most information about an exception and handle it generically. In so doing, the catch statement that uses the most derived type can handle the exception type specifically, accessing data related to the exception and avoiding conditional logic to determine what type of exception occurred.

Therefore, C# enforces the rule that catch blocks appear from most derived to least derived. For example, a catch statement that catches System.Exception cannot appear before a statement catches System.FormatException because System.FormatException derives from System.Exception.

A method could throw many exception types. Table 5.2 lists some of the common ones within the framework.

TABLE 5.2: Common Exception Types

| Exception Type | Description |
| --- | --- |
| System.Exception | The "base" exception from which all other exceptions derive. |
| System.ArgumentException | Indicates that one of the arguments passed into the method is invalid. |
| System.ArgumentNullException | Indicates that a particular argument is null and that this is not a valid value for that parameter. |
| System.Application | To be avoided. The original idea was that you might want to have one kind of handling for system exceptions and another for application exceptions, although plausible, doesnt actually work well in the real world. |