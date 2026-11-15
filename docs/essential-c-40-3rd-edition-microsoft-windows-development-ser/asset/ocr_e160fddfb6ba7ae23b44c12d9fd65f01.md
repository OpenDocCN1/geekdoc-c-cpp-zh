# LISTING 5.16: Declaring Getter and Setter Methods

```
class Employee
{
    private string FirstName;
    // FirstName getter
    public string GetFirstName()
    {
        return FirstName;
    }
    // FirstName setter
    public void SetFirstName(string newFirstName)
    {
        if(newFirstName != null && newFirstName != "")
        {
            FirstName = newFirstName;
        }
    }

    private string LastName;
    // LastName getter
    public string GetLastName()
    {
        return LastName;
    }
    // LastName setter
    public void SetLastName(string newLastName)
    {
        if(newLastName != null && newLastName != "")
        {
            LastName = newLastName;
        }
    }
    // ...
}
```

Unfortunately, this change affects the programmability of the Employee class. No longer can you use the assignment operator to set data within the class, nor can you access data without calling a method.

# Declaring a Property

Considering the frequency of this type of pattern, the C# designers decided to provide explicit syntax for it. This syntax is called a **property** (see Listing 5.17 and Output 5.5).