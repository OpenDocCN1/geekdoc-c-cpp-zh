# LISTING 7.6

continued

```
//-------------------------------------------------------------------
// Constructor: Sets up this student with the specified values.
//-------------------------------------------------------------------
public Student (String first, String last, Address home,
    Address school)
{
    firstName = first;
    lastName = last;
    homeAddress = home;
    schoolAddress = school;
}

//-------------------------------------------------------------------
// Returns a string description of this Student object.
//-------------------------------------------------------------------
public String toString()
{
    String result;

    result = firstName + " " + lastName + "\n";
    result += "Home Address:\n" + homeAddress + "\n";
    result += "School Address:\n" + schoolAddress;

    return result;
}
}
```

The Address class is shown in Listing 7.7. It represents a street address. Note that nothing about the Address class indicates that it is part of a Student object. The Address class is kept generic by design and therefore could be used in any situation in which a street address is needed.

# LISTING 7.7

```
//*******************************************************************
// Address.java      Author: Lewis/Loftus
//
// Represents a street address.
//*******************************************************************
public class Address
{
```