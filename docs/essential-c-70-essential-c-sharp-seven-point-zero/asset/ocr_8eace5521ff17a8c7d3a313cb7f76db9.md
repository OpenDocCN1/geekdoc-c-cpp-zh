ConsoleListControl to display itself. The IListable interface requires a read-only property, ColumnValues.

# **LISTING 8.2: Implementing and Using Interfaces**

```
```csharp
interface IListable
{
    // Return the value of each column in the row
    string[] ColumnValues
    {
        get;
    }
}

public abstract class PdaItem
{
    public PdaItem(string name)
    {
        Name = name;
    }

    public virtual string Name{get;set;}
}

class Contact : PdaItem, IListable
{
    public Contact(string firstName, string lastName,
                   string address, string phone) : base(null)
    {
        FirstName = firstName;
        LastName = lastName;
        Address = address;
        Phone = phone;
    }

    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Address { get; set; }
    public string Phone { get; set; }

    public string[] ColumnValues
    {
        get
        {
            return new string[]
            {
                FirstName,
                LastName,
                Phone,
                Address
            };
        }
    }
}```
```