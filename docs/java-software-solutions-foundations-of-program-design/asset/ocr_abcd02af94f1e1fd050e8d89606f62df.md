# LISTING 10.10 continued

```
//------------------------------------------------------------
// Returns true if the first and last names of this contact match
// those of the parameter.
//------------------------------------------------------------
public boolean equals (Object other)
{
    return (lastName.equals(((Contact)other).getLastName()) &&
            firstName.equals(((Contact)other).getFirstName()));
}

//------------------------------------------------------------
// Uses both last and first names to determine ordering.
//------------------------------------------------------------
public int compareTo (Object other)
{
    int result;

    String otherFirst = ((Contact)other).getFirstName();
    String otherLast = ((Contact)other).getLastName();

    if (lastName.equals(otherLast))
        result = firstName.compareTo(otherFirst);
    else
        result = lastName.compareTo(otherLast);

    return result;
}

//------------------------------------------------------------
// First name accessor.
//------------------------------------------------------------
public String getFirstName ()
{
    return firstName;
}

//------------------------------------------------------------
// Last name accessor.
//------------------------------------------------------------
public String getLastName ()
{
    return lastName;
}
}
```