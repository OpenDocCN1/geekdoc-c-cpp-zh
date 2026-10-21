# Specifying a Type for Enumeration Constants

The constants in a C++/CLI enumeration can be any of the following types:

short int long long long signed char char unsigned unsigned unsigned unsigned unsigned bool short int long long long char

To specify the type for the constants in an enumeration you write the type after the enumeration type name, but separated from it by a colon, just as with the native C++ enum. For example, to specify the enumeration constant type as char, you could write:

```
enum class Face : char {Ace, Two, Three, Four, Five, Six, Seven, Eight, Nine, Ten, Jack, Queen, King};
```

The constants in this enumeration will be of type Char and the underlying fundamental type will be type char. The first constant will correspond to code value 0 by default, and the subsequent values will be assigned in sequence. To get at the underlying value, you must explicitly cast the value to the type.

# Specifying Values for Enumeration Constants

You don’t have to accept the default for the underlying values. You can explicitly assign values to any or all of the constants defined by an enumeration. For example:

```
enum class Face : char {Ace = 1, Two, Three, Four, Five, Six, Seven, Eight, Nine, Ten, Jack, Queen, King};
```

This will result in Ace having the value 1, Two having the value 2, an so on with King having the value 13. If you wanted the values to reflect the relative face card values with Ace high, you could write the enumeration as:

```
enum class Face : char {Ace = 14, Two = 2, Three, Four, Five, Six, Seven, Eight, Nine, Ten, Jack, Queen, King};
```

In this case, Two will have the value 2, and successive constants will have values in sequence so King will still be 13. Ace will be 14, the value you have explicitly assigned.

The values you assign to enumeration constants do not have to be unique. This provides the possibility of using the values of the constants to convey some additional property. For example:

```
enum class WeekDays : bool { Mon =true, Tues = true, Wed = true, Thurs = true, Fri = true, Sat = false, Sun = false };
```

This defines the enumeration WeekDays where the enumeration constants are of type bool. The underlying values have been assigned to identify which represent work days as opposed to rest days.