}
private string? _LastName;
public string? Address { get; set; }

```
public override string GetSummary()
{
    return $"FirstName: { FirstName + NewLine }"
    + $"LastName: { LastName + NewLine }"
    + $"Address: { Address + NewLine }"
}
```

```
// ...
```

```
public class Appointment : PdaItem
{
    public Appointment(string name, string location, DateTime startTimeDateTime, DateTime endDateTime) : base(name)
    {
        Location = location;
        StartDateTime = startTimeDateTime;
        EndTime = endDateTime;
    }

    public DateTime StartDateTime { get; set; }
    public DateTime EndDateTime { get; set; }
    public string Location { get; set; }
}
```

```
// ...
public override string GetSummary()
{
    return $"Subject: { Name + NewLine }"
    + $"Start: { StartDateTime + NewLine }"
    + $"End: { EndDateTime + NewLine }"
    + $"Location: { Location }"
}
```

Listing 7.17 defines the GetSummary() member as abstract, so it doesn't include any implementation. The code then overrides this member within Contact and provides the implementation. Because abstract members are supposed to be overridden, such members are automatically virtual and cannot be declared so