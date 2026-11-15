(a holdover from C++ where the _m_ stands for member variable), as well as the camel-case convention, just as with local variables.³

Regardless of which naming pattern you use for private fields, the coding standard for public fields and properties is Pascal case. Therefore, public properties should use the LastName and FirstName type patterns. Similarly, if no encapsulating property is created around a public field, Pascal case should be used for the field.

# Using Properties with Validation

Notice in Listing 5.19 that the Initialize() method of Employee uses the property rather than the field for assignment as well. Although not required, the result is that any validation within the property setter will be invoked both inside and outside the class. Consider, for example, what would happen if you changed the LastName property so that it checked value for null or an empty string, before assigning it to _lastName.

# LISTING 5.19: Providing Property Validation

```
class Employee
{
    // ...

    public void Initialize(
        string newFirstName,
        string newLastName)
    {
        // Use property inside the Employee
        // class as well.
        FirstName = newFirstName;
        LastName = newLastName;
    }

// LastName property
public string LastName
{
    get
    {
        return _LastName;
    }
    set
```

3. I prefer _firstName because the _m_ in front of the name is unnecessary when compared with simply _, and by using the same casing as the property, it is possible to have only one string within the Visual Studio code template expansion tools, instead of having one for both the property name and the field name.