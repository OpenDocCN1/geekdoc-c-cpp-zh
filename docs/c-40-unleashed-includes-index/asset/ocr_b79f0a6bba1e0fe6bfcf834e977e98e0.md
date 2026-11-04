![](bbox=[0.038, 0.083, 0.77, 0.21])

FIGURE 10.18 Generated files for a LINQ to SQL mapping.

One trimmed-down fragment of the generated code for the Person class looks like this:

```
```csharp
public partial class Person : INotifyPropertyChanging, INotifyPropertyChanged
{
    private int _ID;
    private string _Name;
    private int _Age;

#region Extensibility Method Definitions
    partial void OnNameChanging(string value);
    partial void OnNameChanged();
    ...
#endregion

    public string Name {
        get {
            return this._Name;
        }

        set {
            if ((this._Name != value)) {
                this.OnNameChanging(value);
                this.SendPropertyChanging();
                this._Name = value;
                this.SendPropertyChanged("Name");
                this.OnNameChanged();
            }
        }
    }
    ...
}
```
```