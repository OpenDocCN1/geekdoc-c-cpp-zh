You can now use the Employee class like this:

```
Employee e1 = new Employee()
{
    DateofBirth = new DateTime(1980, 7, 28),
    Name = "Janet",
    Zip = 123456,
    Street = "Kingston Street"
};
Console.WriteLine(e1.Age());
Console.WriteLine(e1.State());
```

# Extending Interfaces

You can extend interfaces if you need to add new members to an existing interface. For example, you might want to define another interface named IManager to store information about managers. Basically, a manager uses the same members defined in the IPerson interface, with perhaps just one more additional property — Dept. In this case, you can define the IManager interface by extending the IPerson interface, like this:

```
interface IPerson
{
    string Name { get; set; }
    DateTime DateofBirth { get; set; }
    ushort Age();
}
```

```
interface IManager : IPerson
{
    string Dept { get; set; }
}
```

To use the IManager interface, you define a Manager class that implements the IManager interface, like this:

```
public class Manager : IManager
{
    //---IPerson---
    public string Name { get; set; }
    public DateTime DateofBirth { get; set; }
    public ushort Age()
    {
        return (ushort)(DateTime.Now.Year - this.DateofBirth.Year);
    }

    //---IManager---
    public string Dept { get; set; }
}
```