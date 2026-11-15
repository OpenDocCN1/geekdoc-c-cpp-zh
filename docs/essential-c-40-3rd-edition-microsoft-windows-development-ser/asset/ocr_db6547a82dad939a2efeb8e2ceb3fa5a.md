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
        return string.Format(
            "*Subject: {0}"+ Environment.NewLine
            + "*Start: {1}"+ Environment.NewLine
            + "*End: {2}"+ Environment.NewLine
            + "*Location: {3}",
            Name, StartDateTime, EndDateTime, Location);
    }
}
```

Listing 6.19 defines the GetSummary() member as abstract, and therefore, it doesn't include any implementation. Then, the code overrides it within Contact and provides the implementation. Because abstract members are supposed to be overridden, such members are automatically virtual and cannot be declared so explicitly. In addition, abstract members cannot be private because derived classes would not be able to see them.

> **Language Contrast: C++ — Pure Virtual Functions**
> 
> C++ allows for the definition of abstract functions using the cryptic notation =0. These functions are called pure virtual functions in C++. In contrast with C#, however, C++ does not require the class itself to have any special declaration. Unlike C#'s abstract class modifier, C++ has no class declaration change when the class includes pure virtual functions.

If you provide no GetSummary() implementation in Contact, the compiler will report an error.