```
```csharp
public Person()             // Constructor with zero arguments
{
}

public Person(string id, string lname, string fname,
              int anAge)   // Constructor with four arguments
{
    idNumber = id;
    lastName = lname;
    firstName = fname;
    age = anAge;
}

public Person(string id, string lname, string fname)
{                             // Constructor with three arguments
    idNumber = id;
    lastName = lname;
    firstName = fname;
}

public Person(string id)
{                             // Constructor with one argument
    idNumber = id;
}

// Read-only property. ID cannot be changed.
public string IDNumber
{
    get
    {
        return idNumber;
    }
}

// Property for last name
public string LastName
{
    get
    {
        return lastName;
    }
    set
    {
        lastName = value;
    }
}

// Read-only property. First name cannot be changed.
public string FirstName
{
    get
    {
        return firstName;
    }
}
```
```