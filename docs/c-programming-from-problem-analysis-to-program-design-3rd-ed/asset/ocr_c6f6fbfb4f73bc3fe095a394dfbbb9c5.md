```
```csharp
public class ShoalArea
{
    private string location;
    private string state;
    private double mileMarker;
    private double[ ] lowTideDepth;
    private double[ ] hiTideDepth;

    public ShoalArea( )
    {
        location = string.Empty;
        state = string.Empty;
        mileMarker = 0;
        lowTideDepth = new double[4];
        hiTideDepth = new double[4];
    }

    public ShoalArea(string loc, string st,
                     double mile, double[ ] low,
                     double[ ] hi)
    {
        location = loc;
        CheckStateOk(st);
        mileMarker = mile;
        lowTideDepth = low;
        hiTideDepth = hi;
    }

    public ShoalArea(string loc, string st,
                     double mile )
    {
        location = loc;
        state = st;
        mileMarker = mile;
    }

    //Properties
    public string Location
    {
        get { return location; }
        set { location = value; }
    }

    public string State
    {
        get { return state; }
        set { CheckStateOk(value); }
    }
}
```
```