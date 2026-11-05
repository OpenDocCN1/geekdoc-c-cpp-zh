```
```csharp
// Properties
private bool Chartered
{
    get
    {
        return chartered;
    }
    set
    {
        chartered = value;
    }
}
private string HouseAddress
{
    get
    {
        return houseAddress;
    }
    set
    {
        houseAddress = value;
    }
}
}
}
```
```

The last class, PresentationGUI, is used to test the components. It is a GUI Windows application. Notice that Figure 11–21 shows that a reference is added to each of the components for the PresentationGUI class. In this class, objects are constructed of the Club, FratSorority, and Intramural classes. The PresentationGUI class includes three RadioButton objects inside a GroupBox object. The radio buttons correspond to the three different types of organization objects being constructed. The source listing for this class follows. Due to space constraints, some of the Windows Forms Designer generated code is omitted. Table 11–2 shows what properties are set for the Form and control objects, and extra comments are added to the source code to aid you in following the example.

**Table 11-2** PresentationGUI property values

| Name | Object type | Property | Value |
|---|---|---|---|
| PresentationGUI | Form | BackColor | Teal |
| PresentationGUI | Form | Font | 12F |
| PresentationGUI | Form | ForeColor | Yellow |