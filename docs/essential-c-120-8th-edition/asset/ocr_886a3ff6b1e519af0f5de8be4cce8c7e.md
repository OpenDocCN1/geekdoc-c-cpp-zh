which evaluates to null. It is not possible to simply return null because there is no implicit conversion from (int Year, int Month, int Day) (the ValueTuple type returned by the other match expressions) and null. Rather, a nullable tuple data type needs to be specified to accurately determine the switch expression's type. (The alternative to the default operator would be to cast ((int Year, int Month, int Day)?)null..

In Listing 7.31, we have four data types that, conceptually similar, have no inheritance relationship between them other than their derivation from object. As such, the only data type available for the input operand is object. Yet, from each we can extract properties for year, month, and day (even if the names don't exist or they vary by the data types). In this case, we extract (int Year, Month, int Day)?, a nullable tuple. And, as long as the tuple is not null, we are able to use the extracted value for year, month, and day into the compositeFormatString value.

# Recursive Pattern Matching (C# 7.0)

LISTING 7.32: Recursive Pattern Matching with the is Operator

```
// ...
Person inigo = new("Inigo", "Montoya");
var buttercup = (FirstName: "Princess", LastName: "Buttercup");

Person inigo, (string FirstName, string LastName) buttercup) couple = (inigo, buttercup);

if (couple is
    // Tuple: Retrieved from deconstructor of Person
    ( // Positional: Select left side or tuple
        { // Property of FirstName
            Length: int inigoFirstNameLength
        }))
```