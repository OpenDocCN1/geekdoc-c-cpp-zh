```
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Address { get; set; }

    public override string GetSummary()
    {
        return @"FirstName: { FirstName + NewLine }"
               + $"LastName: { LastName + NewLine }"
               + $"Address: { Address + NewLine }";
    }
    // ...
}
```

```
public class Appointment : PdaItem
{
    public Appointment(string name) :
        base(name)
    {
        Name = name;
    }

    public DateTime StartDateTime { get; set; }
    public DateTime EndDateTime { get; set; }
    public string Location { get; set; }

    // ...

    public override string GetSummary()
    {
        return $"Subject: { Name + NewLine }"
             + $"Start: { StartDateTime + NewLine }"
             + $"End: { EndDateTime + NewLine }"
             + $"Location: { Location }";
    }
}
```

Listing 7.19 defines the GetSummary() member as abstract, so it doesn’t include any implementation. The code then overrides this member within Contact and provides the implementation. Because abstract members are supposed to be overridden, such members are automatically virtual and cannot be declared so explicitly. In addition, abstract members cannot be private because derived classes would not be able to see them.

It is surprisingly difficult to develop a well-designed object hierarchy. For this reason, when programming abstract types, you should be sure to implement at least one (and preferably more) concrete type that derives from the abstract type to validate the design.