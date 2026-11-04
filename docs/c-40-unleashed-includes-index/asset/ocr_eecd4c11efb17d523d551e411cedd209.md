```
public int Count { get { return _bag.Keys.Count; } }

public override bool TryGetMember(GetMemberBinder binder, out object result)
{
    // Count is never in the bag, so hand over to the C# binder (return false).
    return _bag.TryGetValue(binder.Name, out result);
}

public override bool TrySetMember(SetMemberBinder binder, object value)
{
    if (binder.Name == "Count")
        return false; // Attempt to set Count via the C# binder (will fail).
    _bag[binder.Name] = value;
    return true;
}
```

# EXPANDO OBJECTS

In fact, the concept of objects that can acquire members at runtime is not very novel; after all, dynamic languages such as JavaScript rely heavily on it. In such languages, it's even the case that every single object has those capabilities.

This concept is known as expando objects because they can expand their surface at runtime. The Bag we just built actually exists (in a slightly more sophisticated way) in the System.Dynamic namespace, where it's called ExpandoObject. Additional functionality includes the implementation of INotifyPropertyChanged, as well as direct dictionary access because the type implements IDictionary<string, object>, so it can be used both as a dictionary (with change notification) and through the new dynamic feature:

```
var exp = new ExpandoObject();

// Use as generic dictionary
var dct = (IDictionary<string, object>)exp;
dct["Name"] = "Bart";

// Use as dynamic bag
var bag = (dynamic)exp;
bag.Age = 27;

// Use as enumerable for KeyValuePair<string, object>
foreach (var item in dct)
    Console.WriteLine(item);
```

People familiar with old-school COM programming will recognize the capabilities of the IDispatchEx interface. No wonder this interface was introduced a long time ago to support scripting languages such as VBScript and Jscript.