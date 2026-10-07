# Polymorphism through Interfaces 447

```
public PdaItem(string name)
{
    Name = name;
}
```

```
public virtual string Name { get; set; }

```

```
public class Contact : PdaItem, IListable
{
    public Contact(string firstName, string lastName,
        string address, string phone)
        : base(Getname(firstName, lastName))
    {
        FirstName = firstName;
        LastName = lastName;
        Address = address;
        Phone = phone;
    }
```

```
public string FirstName { get; }
public string LastName { get; }
public string Address { get; }
public string Phone { get; }
static public string GetName(string firstName, string lastName)
    => $"`{firstName} {lastName}";
```

```
public string[] CellValues
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
```

```
public static string[] Headers
{
    get
    {
        return new string[]
        {
            "First Name", "Last Name",
        };
    }
```