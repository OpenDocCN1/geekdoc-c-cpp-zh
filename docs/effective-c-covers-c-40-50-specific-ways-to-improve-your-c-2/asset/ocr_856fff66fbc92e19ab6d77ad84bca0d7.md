The final choice is to provide a wrapper object and export an instance of the wrapper, which minimizes access to the contained object. The System.Collections.ObjectModel.ReadOnlyCollection<T> type is the standard way to wrap a collection and export a read-only version of that data:

```
public class MyBusinessObject
{
    // Read Only property providing access to a
    // private data member:
    private BindingList<ImportantData> listOfData = new
        BindingList<ImportantData>();
    public IBindingList BindingData
    {
        get { return listOfData; }
    }
    public ReadOnlyCollection<ImportantData> CollectionOfData
    {
        get
        {
            return new ReadOnlyCollection<ImportantData>
                (listOfData);
        }
    }
    // other details elided
}
```

Exposing reference types through your public interface allows users of your object to modify its internals without going through the methods and properties you've defined. That seems counterintuitive, which makes it a common mistake. You need to modify your class's interfaces to take into account that you are exporting references rather than values. If you simply return internal data, you've given access to those contained members. Your clients can call any method that is available in your members. You limit that access by exposing private internal data using interfaces, wrapper objects, or value types.

# Item 27: Prefer Making Your Types Serializable

Persistence is a core feature of a type. It's one of those basic elements that no one notices until you neglect to support it. If your type does not support