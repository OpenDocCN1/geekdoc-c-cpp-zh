# # ENUM METHODS

In an amazing bit of compiler sleight-of-hand, the enumerations that you create using the enum keyword are actually instances of a System.Enum class. (Don't let the fact that they're instances of a class confuse you. System.Enum descends from System.ValueType, which makes them value types, not reference types.)

As you know, members are defined in the type, not the instance, and since enumerations are instances, you can't add members to them. But you can reference the members of System.Enum itself, and it has some useful ones:

| String GetName(Type, Object) | Retrieves the name of the constant with the corresponding numeric value inside the specified enumeration |
| String[] GetNames(Type) | Gets an array of all the constant names in the specified enumeration |
| Boolean IsDefined(Type, Object) | Returns a Boolean indicating whether the numeric value provided is defined in the specified enumeration |
| Object Parse(Type, String) | Returns the numeric value of the specified constant name in the specified enumeration |

The constant names in an enumeration must comply with the rules for identifiers, so they're not always as useful as you might like—you wouldn't want to show the user “DoSomething” with no spaces, for example—but it's surprising how often choosing the names carefully can save you a lot of work.

Notice that all of these methods require the enumeration type as a parameter. They're actually static methods that are available from the class itself, not its instances. You can pass the type argument by passing the name of the enumeration wrapped in the GetType() operator, which returns an instance of the System.Type class that represents the type itself.

```
String ConstantName = Enum.GetName(GetType(DayOfTheWeek), 0);
```